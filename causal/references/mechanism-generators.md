# Mechanism generators — prompts for when you're stuck

If step 2 (Mechanism) feels like you're producing labels instead of mechanisms, or step 5 (Alternatives) is producing weak alternatives, use these generators. They force angles you would not naturally take.

## For step 2 (primary mechanism)

When the obvious mechanism is "X is broken," push past it with:

- **"Walk the call stack."** What does the system actually do, step by step, to produce this output? What does each step depend on?
- **"What is the system trying to do at the moment of failure?"** Often the failure happens during a transition (startup, shutdown, reconnect, state change) — not steady state. Name the transition.
- **"What hidden contract is being violated?"** Most failures are a contract mismatch between two components. Name both sides of the contract and the assumption one side is making about the other.
- **"What was the last successful state?"** What was different then? The diff is often the mechanism's trigger.

## For step 5 (alternatives)

When your alternatives feel like watered-down versions of the primary, force a different generator:

- **Different layer.** If your primary is at the application layer, generate one at the OS layer and one at the network layer. (Or: code / config / data / environment / user.)
- **Different timing.** If your primary fires on startup, generate one that fires on shutdown, one on sleep/wake, one on network change.
- **Different actor.** If your primary blames the failing component, generate one that blames a co-resident component, one that blames an upstream service.
- **Cross-domain analogy.** "I have seen this shape of failure before in [different domain] where the cause was X. Does X have an analogue here?"
- **Second-order effect.** What if the visible failure is a *consequence* of a different failure that's invisible? Name the upstream invisible failure.
- **Inverted assumption.** Take your most confident assumption and assume it's false. What mechanism appears?

## For step 3 (conditions)

When your condition list is generic ("network issue," "config issue"), force specificity:

- **What user setting could change this?** Walk through the major settings surfaces the user has touched recently.
- **What did the user install or remove in the last week?** Recent installs/removes are common condition changes.
- **What is co-resident with the failing component?** Other processes, other extensions, other tools sharing the same OS surface.
- **What is the user's network type right now?** Home / office / VPN / hotspot / captive portal — each is a different condition.
- **What is the user's identity / auth state?** Logged in, expired token, MFA pending, conditional access policy applied.
- **What is the time-of-day / load pattern?** Some failures only appear under load, off-hours, or near token-expiry boundaries.

## A meta-prompt for when fully stuck

> "If I were the most cynical, suspicious version of myself reading this analysis, what would I say is the obvious thing the author missed?"

Answer that. The answer is often a real mechanism worth exploring.
