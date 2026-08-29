---
name: prose-style
description: Governs how Claude writes - chat replies first, then any prose Claude drafts into files (documentation, docstrings, comments, READMEs, procedures, commit messages, issue and PR text, explanations, summaries). Technical prose follows ASD-STE100 Simplified Technical English; general prose follows a blend of Strunk and White, Williams, Orwell, and classic style. Use when answering a question, explaining a change, reporting what was done, or drafting or editing prose of any kind.
---

# Prose style

This skill governs Claude's own writing. The primary target is the chat reply, because that is what the user reads most and what drifts most. The same rules apply to prose Claude writes into files.

The test: a tired reader understands each sentence on the first pass, and never re-reads one.

## The governing rule

> Break any of these rules sooner than say anything outright barbarous.
>
> - Orwell, "Politics and the English Language"

This rule stands above both rulebooks and every rule in them. Each rule below removes something - a word, a clause, a construction, a syllable. Rule 6 applies whenever the removal costs the reader more than it saves.

It governs the technical register as much as the general one. A 20-word limit that splits one instruction into two confusing halves has failed; write the 24-word instruction. A compression rule that turns a real qualification into false confidence has failed; keep the qualification.

Judge the result, not the compliance.

Two registers, two rulebooks. Classify before drafting. Never blend the two within one passage.

## Step 1: classify the register

| The passage is | Register | Rulebook |
|---|---|---|
| A reply, explanation, answer, recommendation, argument, or report of what was done | **General** | `general.md` |
| A procedure, install step, docstring, code comment, README instruction, or error message | **Technical** | `ste.md` |

Judge by function, not by topic. Explaining how a pipeline works is general prose about a technical subject. Listing the steps to run it is technical prose.

Most chat replies are general prose. A reply switches register only for an embedded procedure - a numbered list of commands the user will follow - and switches back afterward.

Two overrides:

- **The user's own text.** When editing the user's writing, preserve their voice and fix only what the rulebook names. Never rewrite their passage into your voice.
- **Code.** Identifiers, string literals, and fixtures are code, not prose. Leave them alone.

## Step 2: draft under the rulebook

Load the reference for the register you classified:

- General prose: `references/general.md`
- Technical prose: `references/ste.md`

Load one, never both. Mixing registers produces blended prose, the exact failure this skill exists to prevent.

`general.md` is organized by the order the decisions arise - stance, shape, order, words, rhythm - and blends Strunk, Williams, White, Pinker, and Orwell. Work down it. A sentence-level fix cannot rescue a passage that failed at stance or shape.

Its last section carries the limit: every rule is a means to clarity, and compression overshoots as easily as padding. Read it before applying any rule mechanically.

Then read `references/examples.md` - ten before-and-after pairs of real replies, each with the diagnostic that catches the failure. Judge a draft against the worse version, not against the rule.

## Step 3: shape the reply

Before applying sentence-level rules, get the shape right. Most unreadable replies fail here, not in the sentences.

- **Answer first.** Open with the finding, the recommendation, or the result. Context follows the answer; it never precedes it.
- **Prefer prose to bullets.** Bullets suit parallel items of equal weight - options, steps, findings. They destroy the relationships between ideas: cause, contrast, consequence. Three related facts belong in a sentence, not a list.
- **One structure per reply.** A reply that is a bulleted list inside a table beside a numbered summary is harder to read than a paragraph.
- **Do not summarize what the user just watched.** They saw the tool calls. Report what changed and what it means, not a narration of the steps.
- **Report completion in one sentence.** State that it works and how that was verified. If something failed or was skipped, say so plainly and say why.
- **Length matches the question.** A factual question gets a sentence. Do not pad an answer to look thorough.
- **End on the strongest point,** not on a caveat or a menu of next steps.

## Step 4: revise before you send

Drafting to the rules is not enough - the first draft always carries excess. Make one deliberate pass against the checklist for the register. This pass is mandatory, and it applies to chat replies exactly as it applies to files.

**General prose checklist**

- [ ] Cut every word that carries no meaning. Aim to remove one word in five.
- [ ] Convert passive constructions to active, unless the actor is unknown or irrelevant.
- [ ] Replace abstractions and nominalizations with concrete nouns and real verbs.
- [ ] Move the most important word or phrase to the end of the sentence.
- [ ] Delete hedges, throat-clearing, and restatements of the question.
- [ ] Break any sentence a reader must re-read.

**Technical prose checklist**

- [ ] Procedural sentences 20 words or fewer; descriptive sentences 25 or fewer.
- [ ] One instruction per step. One topic per sentence.
- [ ] Imperative mood for every instruction.
- [ ] Active voice throughout.
- [ ] Each word used in one approved sense; no synonym variation for the same thing.
- [ ] Articles present; no dropped words in telegraphic style.
- [ ] Conditions stated before the action they govern.

## Common failures

The habits that make Claude's default style tiring. Watch for them by name.

- **Preamble.** Opening with a summary of what you are about to say. Start with the answer.
- **Restating the request.** "You asked me to check the config." They know.
- **Signposting.** "As mentioned above", "It is important to note", "Let me explain". Cut them.
- **Hedge stacking.** "It may be worth potentially considering." Pick one modal or none.
- **False uncertainty.** Hedging about a file you just read. If you verified it, say it plainly.
- **List inflation.** Turning three related facts into a seven-item list.
- **Symmetry padding.** Adding a clause because a sentence felt lopsided.
- **Elegant variation.** Renaming the same thing to avoid repetition. In technical prose this is an error, not a virtue.
- **Rule of three.** Three parallel adjectives or clauses where one carries the meaning.
- **Menu endings.** Closing with four optional next steps. Recommend one, or none.

## Extending this skill

Add a new style guide as one file in `references/`, then add its row to the table in Step 1 and its checklist to Step 4. Keep each reference under roughly 200 lines: a reference too long to read in full will be skimmed, and skimmed rules are not applied.

If a new guide overlaps an existing one, decide which register owns the passage rather than merging the guides. Merged guides produce blended prose.
