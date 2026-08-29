# Technical prose: ASD-STE100 Simplified Technical English

For documentation, docstrings, code comments, READMEs, procedures, method steps, install guides, and error messages.

STE was written so that a reader with limited English can follow safety-critical instructions without ambiguity. It trades elegance for certainty. Do not use it for argument or explanation.

Reference: https://github.com/danyuchn/asd-ste100-skill

## The core constraints

**One word, one meaning.** Each word carries a single approved sense throughout the document. *Follow* means "come after", never "obey". *Fit* means "install", never "be the correct size". If you need the other meaning, choose a different word.

**One meaning, one word.** Never vary the term for a thing. If it is a *connector* in step 1, it is a *connector* in step 9. Elegant variation is an error here, not a virtue.

**One topic per sentence.** Split any sentence carrying two ideas.

**One instruction per step.** A step with two verbs is two steps.

**Short sentences.** Procedural sentences: 20 words maximum. Descriptive sentences: 25 words maximum.

**Short paragraphs.** Procedural paragraphs: 6 sentences maximum. Descriptive paragraphs: 10 maximum.

## Grammar

- **Use the active voice.** "Set the flag" not "the flag should be set".
- **Use the imperative for instructions.** Start the step with the verb.
- **Keep articles.** Write "Open the file", not "Open file". Telegraphic style creates ambiguity.
- **Use approved verb forms only:** infinitive, imperative, simple present, simple past, simple future, and the past participle used as an adjective. Avoid progressive tenses and gerunds.
- **Avoid noun clusters of more than three nouns.** "Database connection pool timeout configuration value" is unreadable. Break it with prepositions: "the timeout value for the database connection pool".
- **State the condition before the action.** "If the file exists, delete it" - not "Delete the file if it exists". The reader must know whether to act before reading the action.
- **Write one thought per sentence, in the order the reader needs it.** Time order for steps, cause before effect.
- **Do not use slang, idiom, or metaphor.** "Kill the process" is idiom; "Stop the process" is instruction.
- **Do not use parenthetical asides** inside a step. Move them to a following note.

## Word substitutions

| Avoid | Use |
|---|---|
| utilize, employ (as verb) | use |
| perform, execute, conduct | do, run, start |
| commence, initiate | start |
| terminate, cease | stop, end |
| prior to, in advance of | before |
| subsequent to, following | after |
| in the event that | if |
| in order to | to |
| a number of, a variety of | some, several, or a count |
| approximately | about |
| assist | help |
| attempt | try |
| obtain, acquire | get |
| provide | give |
| require | need |
| indicate | show |
| verify, validate | check, make sure |
| modify | change |
| additional | more, other |
| sufficient | enough |
| in the vicinity of | near |
| at this time | now |
| it is possible to | you can |
| should be able to | can |

## Notes, cautions, and warnings

Keep the three distinct and use them consistently:

- **Note:** information that helps, but no risk.
- **Caution:** an action that can damage data or equipment.
- **Warning:** an action that can injure a person.

Put the warning before the step it governs, never after. State the hazard, then the consequence, then the avoidance.

## Docstrings and comments

- Describe what the function does, in the present simple: "Returns the parsed record." One sentence, then a blank line, then detail.
- Document the contract, not the implementation. The implementation is visible; the contract is not.
- Write comments to explain *why*, never *what*. A comment restating the code is noise that will drift out of date.
- Use the same term as the identifier. If the parameter is `timeout_seconds`, the docstring says "timeout in seconds", not "wait period".

## What STE does not cover

STE has no rules for argument, emphasis, or narrative flow, because it forbids them. When a passage must persuade or explain rather than instruct, it is general prose. Switch to `strunk-white.md`.
