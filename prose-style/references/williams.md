# General prose: Williams, *Style: Lessons in Clarity and Grace*

Companion to `strunk-white.md`, not a replacement. Strunk says what to cut. Williams says how to order what remains.

Every rule here comes with a diagnostic you can run on one sentence. Use them when a sentence obeys Strunk yet still reads badly - that failure is almost always an ordering failure.

## 1. Characters as subjects, actions as verbs

A sentence is clear when its grammatical subject names the character doing something, and its verb names what that character does.

Prose turns opaque when the action hides inside an abstract noun - a nominalization - and the verb slot fills with a placeholder: *is*, *has*, *makes*, *performs*, *provides*, *occurs*.

**Diagnostic.** Underline the first seven or eight words. If they contain no concrete character and no real action, revise.

**Revision.** Find the action, wherever it hides. Make it the verb. Find who or what performs it. Make that the subject.

| Nominalized | Recovered |
|---|---|
| Our discussion of the problem led to a resolution. | We discussed the problem and resolved it. |
| The failure of the parser is due to an absence of validation. | The parser fails because nothing validates the input. |
| There was an expectation on the part of reviewers that... | Reviewers expected that... |
| Performance of the analysis was done by the script. | The script analyzed the data. |

Three signals that a nominalization is present: a noun ending in *-tion*, *-ment*, *-ance*, *-ity*, or *-ness*; the verb *is* linking two abstractions; an empty subject, *there is* or *it is*.

Keep a nominalization when it names something the reader already knows, when it refers to a previous sentence (*This failure led to...*), or when it is the accepted term for the thing (*regression*, *randomization*).

This rule explains the passive-voice advice rather than repeating it. The passive is bad when it hides the character. When the character is unknown, irrelevant, or already known, the passive is correct - and in methods sections it is often the honest choice.

## 2. Topic position: old information first

The first few words of a sentence tell the reader what the sentence is about. Put there what the reader already knows - a term from the preceding sentence, a name already introduced. New information belongs later.

A paragraph reads as connected when consecutive sentences open with related topics. It reads as disjointed when each sentence opens with something new, even if every sentence is individually clear.

**Diagnostic.** Read only the first four or five words of each sentence in a paragraph. If that sequence does not form a consistent thread, the paragraph will feel disconnected no matter how you polish the sentences.

This is why signposting is unnecessary. "As mentioned above" is a patch over a topic string that fails to connect. Fix the string and the patch becomes redundant.

## 3. Stress position: new information last

The end of a sentence carries the greatest weight. Put the news there - the point, the number, the name, the consequence.

Two habits destroy the stress position. Trailing qualifications (*..., which is something to keep in mind*) bury the point behind throat-clearing. Trailing prepositional pile-ups (*...in the configuration file for the deployment environment*) end the sentence on machinery.

**Diagnostic.** Read the last four words aloud. If they are not what you want the reader to carry away, move what is.

**Revision.** Shift the qualification to the front or into its own sentence. Trim the tail so the sentence lands on the news.

## 4. Cohesion and coherence are different problems

**Cohesion** is the join between two consecutive sentences: old-to-new, sentence by sentence. It is local, and rules 2 and 3 govern it.

**Coherence** is whether a whole passage is about something. A passage is coherent when its sentences share a small set of topics, when it states its point somewhere the reader will find it, and when that point governs everything around it.

**Diagnostic for coherence.** Underline the point sentence of the paragraph. If none exists, write one. If it sits at the end of a long paragraph and the paragraph opens, then the reader read the whole paragraph without knowing what it was for - move it up.

For a reply, the point belongs in the first sentence. For a paragraph inside a longer explanation, the point belongs first or immediately after a short setup.

## 5. Complexity belongs at the end

Readers hold a sentence in memory until the subject meets its verb. Long subjects, interruptions between subject and verb, and stacked front-loaded conditions all force the reader to carry an unresolved load.

Get to the verb early. Put the long, complex, list-like material at the end, where the reader can unload it as it arrives.

| Front-loaded | Reordered |
|---|---|
| That the parser silently drops malformed rows rather than raising is the problem. | The problem is that the parser silently drops malformed rows rather than raising. |
| Timeouts, retries, and connection-pool limits, which interact in ways that are hard to predict, are configured here. | This file configures timeouts, retries, and connection-pool limits, which interact unpredictably. |

## 6. Concision, as a procedure

Strunk's rule with steps attached. Delete in this order:

1. Words that mean nothing: *actually*, *basically*, *certainly*, *generally*, *really*, *various*, *particular*.
2. Words implied by other words: *each and every*, *full and complete*, *first and foremost*, *terrible tragedy*, *free gift*.
3. Phrases replaceable by one word: *in the event that* to *if*, *for the purpose of* to *to*, *in the vicinity of* to *near*.
4. Metadiscourse - commentary on your own writing: *it should be noted that*, *it is interesting that*, *what I want to emphasize is*.
5. Belaboring the obvious: sentences the reader could have written themselves.

## 7. The limit

Williams ends where Strunk ends: these are principles, not laws. A rule that produces a worse sentence has failed its own purpose. Clarity serves the reader, and when the reader is served better by a long sentence, an abstraction, or a passive, write it.

Judge the result, not the compliance.
