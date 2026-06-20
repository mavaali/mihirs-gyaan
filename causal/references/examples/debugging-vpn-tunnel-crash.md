# Example: VPN tunnel crash loop

A worked example showing the skill applied to a real debugging session. The "before" shows the single-link causal failure mode; the "after" shows the five-step chain finding the actual root cause.

## Setup

User reports: "the VPN client cannot connect to the internet."

After triage: pausing the VPN client restores internet. With the VPN client active, internet breaks. Crash reports show the VPN tunnel system extension crashing with SIGABRT during `NEExtensionAppProxyProviderContext stopWithReason:`, triggered by a failed `NSFileHandle readDataUpToLength:` over XPC. Crashes recur every 2–12 minutes.

## Before (single-link causation — wrong)

> "The crash signature is in the extension's stop path, with an uncaught Objective-C exception during XPC teardown. This is a vendor bug in VPN client x.y.z. File a ticket with IT, attach the .ips file, request a client update."

This is a category-as-cause: "vendor bug." It is not falsifiable, does not predict when the crash will or won't happen, and stops investigation at the first plausible label.

## After (five-step chain — right)

### Effect
- VPN client active → all internet traffic fails (DNS + HTTPS both blocked)
- VPN client paused → internet works normally
- Tunnel system extension crashes with SIGABRT every 2–12 minutes when active
- Crash backtrace: `stopWithReason:` → `NSFileHandle readDataUpToLength:` → uncaught NSException
- Crash cluster aligns with user-initiated toggles (channel disable/enable, client quit)
- Independent of network type (reproduces on home Wi-Fi)

### Mechanism
The VPN tunnel extension uses an XPC connection to coordinate with the VPN client. During teardown (`stopWithReason:`), the extension reads remaining buffered data from the XPC pipe with `NSFileHandle readDataUpToLength:`. If the read fails or returns malformed data, NSFileHandle raises an Objective-C exception. The extension does not catch this exception in the teardown path, so it propagates to the runtime and triggers `abort()`.

The teardown path runs whenever the extension is asked to stop — channel toggle, client quit, network change, sleep/wake — *or* whenever the extension itself decides to restart due to internal error state.

So: anything that puts the extension into an error state that triggers a self-restart will hit the teardown path, fail the XPC read, and crash.

### Conditions required
For the mechanism to fire, one of these must hold:
- (a) Something is interfering with the data the VPN client expects to see on its DNS classification surface (DNS not visible → classifier hits error state → triggers self-restart → crashes in teardown)
- (b) Another network extension is racing the VPN client for the tunnel layer (co-resident: another security agent's network extension is also active)
- (c) A stale forwarding profile is producing malformed responses (rules out: reboot pulled fresh profile)
- (d) macOS NetworkExtension framework regression in 26.5.x specifically affecting `NSFileHandle` over XPC during stop

### Environment check
- (a) **Confirmed present.** User has encrypted DNS (DoH/DoT) configured on the active Wi-Fi network. Encrypted DNS routes queries directly to Cloudflare/Google over HTTPS, bypassing the system resolver. the VPN client's Internet Access channel intercepts plain DNS to classify destinations; with encrypted DNS, it sees no queries to classify and hits error paths.
- (b) Confirmed present (the other security agent extension is active), but no evidence of contention in logs. Lower probability.
- (c) Ruled out (post-reboot fresh profile, same behavior).
- (d) Unknown — would require Apple-side investigation. Lower probability given (a) is sufficient to explain the effect.

### Alternatives considered
1. **Pure vendor bug (no environment trigger)** — would predict crashes happen on any the VPN client install on macOS 26.5.x at the same frequency. Distinguishing test: do other users with the VPN client + macOS 26.5.x see this rate? Likely no — would be a known issue by now.
2. **the other security agent extension contention** — would predict the crash happens on traffic events, not stop events. Backtrace shows stop path. Ruled out as primary.
3. **Captive portal / network identity issue** — would predict location-dependence. Reproduces on home Wi-Fi. Ruled out.

### Conclusion
Candidate root cause: **encrypted DNS on the active Wi-Fi network is preventing the VPN client's DNS classifier from operating, putting the extension into a restart loop where the stop path crashes on XPC read.**

**Confidence: High** — removing encrypted DNS eliminated crashes and restored stable operation. Mechanism + condition + test all align. The vendor bug is still real (the stop path should not crash on a recoverable read failure), but the trigger is environmental, and the user fix is to leave encrypted DNS off on networks where the VPN client is in use.

## Why the chain found what single-link missed

The single-link answer stopped at the crash signature. The chain forced the question: *what conditions would make this signature appear?* That question routed straight to DNS interception, which routed to encrypted DNS, which the user had recently enabled.

The crash signature is downstream; the encrypted DNS toggle is upstream. Single-link reasoning sees only downstream and labels it "vendor bug." Pearl discipline walks upstream until it finds something the user can change.
