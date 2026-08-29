# prose-style

A Claude Code skill that governs how Claude writes to you: chat replies first, then documentation, docstrings, comments, commit messages, and anything else it drafts.

Claude's default style is hard to read for specific, nameable reasons - preamble before the answer, tool calls narrated back to you, three facts inflated into seven bullets, hedges on facts it just verified, and a menu of next steps at the end. This skill names those habits, supplies one rulebook, and requires a revision pass before output.

## What it does

The skill works through two levers, because one is not enough.

`SKILL.md` and its references load on demand, when Claude judges a task to be about writing. They carry the full rulebook and the worked examples.

A short block in `~/.claude/CLAUDE.md` loads every turn. It holds the reply-shape rules and the prohibitions, because an ordinary reply never announces itself as a writing task, and the skill will not fire on it. This costs about 150 tokens per turn and is the part that governs conversation.

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

## How it is built

**One rulebook, not one per source.** `general.md` is organized by the order decisions arise - stance, shape, order, words, rhythm - and blends Strunk and White, Williams, White's rhythm chapter, Pinker, and Orwell at the section each is strongest. Organizing by source produced a file that argued with itself.

**Correct guidance only.** Where guides conflict, the file states the resolved rule once. It never quotes a rule and then explains why to ignore it. Orwell's blanket ban on the passive is absent; Williams's actual rule - the passive fails when it hides who acted - is present.

**Two passes, not one.** Pass 1 cuts. Pass 2 asks what the cutting cost: compressed lists that should have stayed lists, actors erased by the passive, announced counts that were never counted, uncertainty deleted into false confidence. Every rule in the file removes something, and without Pass 2 nothing tells Claude when to stop.

**Orwell's sixth rule governs.** *Break any of these rules sooner than say anything outright barbarous.* It sits above both the rulebook and the checklist, because a rule that costs the reader more than it saves has failed.

**Examples over rules.** Rules describe a target; examples calibrate one. Seven of the seventeen pairs are real failures caught during development, including two the rulebook had no name for until they happened.

## Extending it

Fold a new guide into `references/general.md` at the section that owns the decision. Do not add a file per source. If the new guide contradicts one already there, state the resolved rule once and delete the loser.

Add examples from replies that actually annoyed you. Save the reply, write the revision beside it, name the failure, and state the diagnostic in one sentence. An invented failure is always a little too obvious to be useful.

## Sources

Strunk and White, *The Elements of Style*, including White's "An Approach to Style". Joseph Williams, *Style: Lessons in Clarity and Grace*. Steven Pinker, *The Sense of Style*. Thomas and Turner, *Clear and Simple as the Truth*. George Orwell, "Politics and the English Language". Garner's *Modern English Usage* settles disputed usage.
