---
name: prose-style
description: Apply a register-aware prose style to anything written for a human reader - chat replies, manuscripts, abstracts, grants, documentation, docstrings, comments, READMEs, procedures, commit messages, and issue text. Technical prose follows ASD-STE100 Simplified Technical English; general prose follows Strunk and White. Use whenever drafting, editing, reviewing, or being asked to make writing clearer, shorter, or easier to read.
---

# Prose style

Write so a tired reader understands the sentence on the first pass.

Two registers, two rulebooks. Classify the passage before drafting. Never blend the two within one passage.

## Step 1: classify the register

| The passage is | Register | Rulebook |
|---|---|---|
| Manuscript, abstract, grant, discussion, argument, explanation, narrative, chat reply | **General** | Strunk and White |
| Documentation, docstring, code comment, README, procedure, method step, install guide, error message | **Technical** | ASD-STE100 |

Judge by function, not by topic. An explanation of how a pipeline works is general prose about a technical subject. A numbered list of steps to run that pipeline is technical prose.

A document may contain both. A README's opening paragraph explains and persuades; its install steps instruct. Switch register at the section boundary, not mid-paragraph.

Two cases override the table:

- **Quoted or edited text.** When revising the user's own writing, preserve their voice and fix only what the rulebook names. Do not rewrite a passage into your voice.
- **Code.** Identifiers, string literals, and test fixtures are code, not prose. Leave them alone.

## Step 2: draft under the rulebook

Load the reference for the register you classified:

- General prose: `references/strunk-white.md`
- Technical prose: `references/ste.md`

Do not load both. Loading the wrong one produces blended prose, the exact failure this skill exists to prevent.

## Step 3: revise before you output

Drafting to the rules is not enough - the first draft always carries excess. Make one deliberate pass against the checklist for the register. This pass is mandatory, including for chat replies.

**General prose checklist**

- [ ] Cut every word that carries no meaning. Aim to remove one word in five.
- [ ] Convert passive constructions to active, unless the actor is genuinely unknown or irrelevant.
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

These are the habits that make the default style hard to read. Watch for them by name.

- **Preamble.** Opening with a summary of what you are about to say. Start with the answer.
- **Symmetry padding.** Adding a clause because a sentence felt lopsided.
- **Hedge stacking.** "It may be worth potentially considering." Pick one modal or none.
- **Elegant variation.** Renaming the same thing to avoid repetition. In technical prose this is an error, not a virtue.
- **List inflation.** Turning three related facts into a seven-item bulleted list. Prose carries relationships that bullets destroy.
- **Signposting.** "As mentioned above", "It is important to note". Cut them; the reader can see the page.
- **Rule of three.** Three parallel adjectives or clauses where one carries the meaning.

## Extending this skill

Add a new style guide as one file in `references/`, then add its row to the table in Step 1 and its checklist to Step 3. Keep each reference under roughly 200 lines: a reference too long to read in full will be skimmed, and skimmed rules are not applied.

If a new guide overlaps an existing one, decide which register owns the passage rather than merging the guides. Merged guides produce blended prose.
