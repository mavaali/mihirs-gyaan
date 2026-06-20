# Rubric — waglesworld blog voice (worked example)

A complete, real rubric for `autoresearch-writing`. It is calibrated to one author's
published blog voice (essays on AI/product on waglesworld.com). **It is an example, not a
default to use blindly** — the dimensions, anti-patterns, and anchors are this author's. To
use the loop on your own writing, build your own from [rubric.example.md](./rubric.example.md).

- **Dimensions:** 9, scored 1–5. **Total: /45. Target: ≥ 40/45.**
- **Tie-break order for "lowest dimension":** Taste, then Earned Reveal.

## Dimensions

### 1. Earned Reveal
The opening establishes a tension the piece resolves. Two valid patterns — score against
whichever it uses:

- **Pattern A — Frame Reset:** opener names the dominant/wrong frame and pivots to the real
  one within ~150 words.
  - **5:** "AI didn't create a skills crisis for PMs, it exposed a measurement crisis." Names
    the belief, dismantles it, lands the real frame in the opening.
  - **3:** pivots eventually, or the reset is implied not stated.
  - **1:** standard expository opener, no reset.
- **Pattern B — Hypothesis Falsification:** opener states a curiosity/hypothesis/assumption
  the piece then tests and overturns.
  - **5:** "I wanted to know what it costs... none of it was real... Three things I got wrong."
  - **3:** hypothesis stated but falsification is vague.
  - **1:** no clear prior, just an expository tour of findings.

If the piece uses neither pattern → max score 3.

### 2. Load-Bearing Structure
ONE thing structurally carries the argument. Four valid spines: cross-domain analogy; data
narrative; personal experiment; historical/precedent parallel.
- **5:** ONE clear spine; removing it collapses the argument; no competing spines.
- **3:** spine carries only part of the piece, or two spine types partially overlap.
- **1:** no discernible spine, OR multiple competing spines.

Spine types can mix coherently if they serve one idea. Score on coherence, not type purity.

### 3. Sourced Numbers
Every substantive claim backed by specific, attributable data.
- **5:** numbers with a named source ("Mollick et al. 43%/17%", "99.6% cache hit rate from
  8,761 events"). Citations are load-bearing.
- **3:** some numbers, partial or vague sourcing ("studies show").
- **1:** vibes-only; no data, or data without provenance.

### 4. Falsifiable Structure
The argument states what would prove it wrong, or the claim was built and measured.
- **5:** explicit experiment with stated priors and outcomes, or named conditions.
- **3:** implied falsifiability; a clear bet but no explicit conditions.
- **1:** untestable ("AI will transform everything").

### 5. Headings as Claims
Each H2/H3 is a micro-argument, not a label.
- **5:** "The Employee Model Fails at the Boundary" / "The proxy was 300x wrong."
- **3:** mix of claim-headings and label-headings.
- **1:** all labels: "Background" / "Analysis" / "Conclusion".

### 6. Rhythm Variance
Long sentence followed by short fragment. Read-aloud test.
- **5:** cadence audible. "The scaffolding shipped. The measurement didn't." Fragments for
  emphasis, not constantly.
- **3:** mostly even lengths, occasional fragment; rhythm broken by table/bullet density.
- **1:** walls of equal-length sentences, no fragments.

### 7. Landed Claims
Uncomfortable points stated without hedging. No "might", "could potentially", "in some sense",
"arguably", "I think", "perhaps", "it seems".
- **5:** "This is directionally correct and practically useless." Clean.
- **3:** most claims clean, 1–2 hedges leak in.
- **1:** hedge-laden throughout.

"Might" used to flag genuine variance ("your number might differ") is not a hedge of the claim.

### 8. Consequence Ending
Closes with an instruction, prediction, or unresolved tension. Never a summary.
- **5:** "Start building a track record of decisions, not deliverables." Reader leaves with
  action or warning.
- **3:** mild forward-looking statement, but reads partly like recap.
- **1:** "In conclusion..." / "To summarize..."

### 9. Taste — engaging without being superficial
The hardest dimension. Score via pairwise comparison vs. the calibration anchor. Sub-criteria:
trusts the reader; reframe is earned (conclusion of an argument, not its premise); no flattery
of reader/self/topic; references are load-bearing; costs something to publish; one layer past
the obvious take.
- **5:** hits all six. **3:** hits three. **1:** listicle / clickbait reframe / reader-flattery
  / asserted-not-earned reframe.

## Anti-patterns — appearance triggers a HARD REVERT

- Em dashes (—) anywhere
- Hedging language: "might", "could potentially", "in some sense", "arguably", "perhaps",
  "I think", "I believe", "it seems" (when hedging the claim, not flagging genuine variance)
- "My take:" used more than once
- Listicle structure ("5 reasons...", "3 things you need to know")
- Reader flattery ("if you're reading this you already get it", "smart PMs know...")
- Authority flattery ("as Karpathy brilliantly noted", "the great X once said")
- Opening with a question
- Generic AI-speak ("in today's rapidly evolving landscape", "leverage", "robust", "seamless")
- Two competing spines
- "In conclusion" / "To summarize"
- Emoji headings
- Bullet lists where prose would carry the rhythm

## Calibration anchors (5/5 reference pieces)

- Frame Reset spine: https://www.waglesworld.com/blog/the-measurement-crisis (44/45)
- Hypothesis Falsification spine: https://www.waglesworld.com/blog/where-your-ai-tokens-actually-go (~43/45)

Discrimination matters more than absolute scores: the rubric should rank a strong piece above
a weaker one. If it doesn't, the rubric is wrong, not the piece.

### Snippet anchors

- **Earned Reveal A:** "AI didn't create a skills crisis for PMs, it exposed a measurement
  crisis that was already there."
- **Earned Reveal B:** "I wanted to know what it costs... none of it was real... Three things
  I got wrong."
- **Sourced Numbers:** "Mollick et al. found that AI lifted bottom-half consultants'
  performance by 43% while top performers gained only 17%."
- **Landed Claims:** "This is directionally correct and practically useless."
- **Consequence Ending:** "The scaffolding shipped. The measurement didn't."
