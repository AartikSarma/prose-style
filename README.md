# prose-style

A Claude Code skill that governs how Claude writes to you: chat replies first, then documentation, docstrings, comments, commit messages, and anything else it drafts.

Claude's default style is hard to read for specific, nameable reasons - preamble before the answer, tool calls narrated back to you, three facts inflated into seven bullets, hedges on facts it just verified, and a menu of next steps at the end. This skill names those habits, supplies one rulebook, and requires a revision pass before output.

## What it does

Ask Claude why a test fails and you get the answer in the first sentence, not in the fifth:

> **Before:** Great question! Let me look at the test suite. I ran pytest, checked the config, and examined the failing assertion. Based on my analysis, the fixture is the problem.
>
> **After:** Three tests fail on one fixture: `make_patient()` returns no `admit_time`, so every length-of-stay assertion is null.

The skill installs in two places, because either alone leaves a gap.

`prose-style/SKILL.md` and its references load on demand, when Claude judges a task to be about writing. They carry the full rulebook and the worked examples - too much text to keep in context permanently.

A four-line block in `~/.claude/CLAUDE.md` loads on every turn instead. An ordinary reply never announces itself as a writing task, so the skill alone would never fire on the conversation itself. Those four lines cost about 150 tokens per turn and cover the case that matters most.

## Install

1. Clone this repository.
2. Symlink the skill into your Claude directory:

   ```sh
   ln -s "$PWD/prose-style" ~/.claude/skills/prose-style
   ```

3. Copy the block from `claude-md-snippet.md` into `~/.claude/CLAUDE.md`.
4. Start a new Claude Code session. Run `/prose-style` to confirm the skill loads.

The symlink keeps one source of truth: edit the files here and every project sees the change.

## Contents

| File | Holds |
|---|---|
| `prose-style/SKILL.md` | The governing rule, reply shape, and the two-pass revision checklist |
| `prose-style/references/general.md` | The rulebook, ordered by the decisions a writer makes |
| `prose-style/references/examples.md` | Seventeen before-and-after pairs, each with a diagnostic |

## How it works

Claude runs three things in order. Getting the shape right comes first, because a passage that opens in the wrong place cannot be rescued by fixing its sentences.

**Shape.** Answer first, context after. Length matches the question. Prose where ideas connect by cause or contrast; bullets only for items of equal weight. No narrating tool calls the reader just watched, and no closing menu of optional next steps.

**Draft**, using `references/general.md`. The rulebook is ordered by the decisions a writer actually makes, not by the guides it draws on:

| Decide | Ask |
|---|---|
| Stance | What am I showing the reader, and what do they already know? |
| Shape | Where does the point go? First. |
| Order | Does each sentence open with old information and end with the news? |
| Words | Does every word do work? |
| Rhythm | Does the sentence length vary enough to stay readable? |

**Revise, in two passes.** Pass 1 cuts: needless words, nominalizations, hedges, passive constructions that hide who acted. Pass 2 asks what the cutting cost, and it exists because every rule in Pass 1 removes something:

> *The files were folded into one and the shape rules were moved to always-on config.*

That sentence obeys Pass 1 - short, no padding - and fails Pass 2, which asks whether the actor survived. In a report of shared work, who decided is the substance: *I folded the files, and you moved the shape rules.*

Pass 2 also catches lists compressed into prose until they need unpacking, counts announced without counting, and hedges cut until a guess reads as a certainty.

## Three properties worth knowing

**Every rule carries its limit.** "Prefer prose to bullets" is followed, in the same paragraph, by the failure that comes from over-applying it: parallel items of equal weight crammed into one sentence with semicolons, producing a long clause with no working verb. A rule stated one-directionally has no stopping condition, and Claude will run it off a cliff.

**Where guides disagree, the file states one rule.** Orwell says never use the passive; Williams says the passive fails only when it hides who acted. The rulebook carries Williams's version alone. It never quotes a rule and then explains why to ignore it, because a reader following instructions should not have to adjudicate between them. So *we measured the flow rate* replaces *measurements were obtained*, while *the samples were stored at -80 C* stands - nobody needs the actor.

**One rule governs the rest**, from Orwell: *break any of these rules sooner than say anything outright barbarous*. Every other rule removes something, and this one applies whenever the removal costs the reader more than it saves. A 20-word sentence limit that splits one instruction into two confusing halves has failed; write the 24-word instruction.

## Why the examples matter

Rules describe a target. Examples calibrate one. `references/examples.md` holds seventeen pairs, each a real failure with its revision and a one-line diagnostic:

> **Before:** It seems like it may be possible that the config file might not be getting loaded correctly, though I'd need to verify this further.
>
> **After:** The config never loads: `load_config()` reads `./config.yaml`, but the file is at `./conf/config.yaml`.
>
> *Diagnostic: did you read it or run it? Then state it.*

Seven of the seventeen came from Claude's own replies while the skill was being written, including two failures the rulebook had no name for until they appeared - restating a file it had just written, and announcing that it had run a check.

## Extending it

Fold a new guide into `references/general.md` at the section that owns the decision. Do not add a file per source. If the new guide contradicts one already there, state the resolved rule once and delete the loser.

Add examples from replies that actually annoyed you. Save the reply, write the revision beside it, name the failure, and state the diagnostic in one sentence. An invented failure is always a little too obvious to be useful.

## Sources

Strunk and White, *The Elements of Style*, including White's "An Approach to Style". Joseph Williams, *Style: Lessons in Clarity and Grace*. Steven Pinker, *The Sense of Style*. Thomas and Turner, *Clear and Simple as the Truth*. George Orwell, "Politics and the English Language". Garner's *Modern English Usage* settles disputed usage.
