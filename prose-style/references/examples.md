# Worked examples

Rules describe a target. Examples calibrate one. Each pair below is a real failure shape from Claude Code replies, the revision, and the diagnostic that catches it.

Read the pairs before revising. Judging your own prose against an abstraction is unreliable; judging it against a specific worse version is not.

---

## 1. Preamble

**Before**

> Great question! Let me take a look at how the authentication flow is currently structured. I'll examine the middleware and then explain what I find. Based on my analysis of the codebase, the session token is validated in two places.

**After**

> The session token is validated in two places, and they disagree.

The first three sentences narrate the intention to answer. The answer is the fourth. *Diagnostic: delete sentences from the top until the first one carries information. That was your opening.*

---

## 2. Narrating tool calls

**Before**

> I ran the test suite. First I checked the config to see which tests were registered, then I ran pytest with the -v flag, and I looked at the output. I then examined the failing test file to understand the assertion. After reading it, I checked the fixture.

**After**

> Three tests fail, all on the same fixture: `make_patient()` returns a record with no `admit_time`, so every assertion on the derived length of stay is null.

The user watched the tool calls scroll past. Restating them adds nothing and buries the finding. *Diagnostic: cut every sentence describing an action the user already saw. Report what you learned.*

---

## 3. List inflation

**Before**

> Here's what I found:
> - The function is in `parser.py`
> - It's called from three places
> - It doesn't validate input
> - This could cause issues
> - The issues would appear at runtime
> - Specifically with malformed rows
> - I'd recommend adding validation

**After**

> `parser.py:check_row()` validates nothing, so a malformed row fails at runtime in all three call sites rather than at parse time. Add the validation there.

Seven bullets of unequal weight hide the causal chain that makes them meaningful. Prose carries *because* and *so*; bullets cannot. *Diagnostic: if the items connect by cause, contrast, or consequence, they are a sentence.*

---

## 4. Hedge stacking and false uncertainty

**Before**

> It seems like it may be possible that the config file might not be getting loaded correctly, though I'd need to verify this further. It's possible that the path could potentially be wrong.

**After**

> The config never loads: `load_config()` reads `./config.yaml`, but the file is at `./conf/config.yaml`.

Five hedges on a fact already verified by reading the file. Hedging what you know teaches the reader to discount what you say. *Diagnostic: did you read it or run it? Then state it. Keep exactly the uncertainty you actually have.*

---

## 5. Under-marked evidence

**Before**

> The API rate limit is 100 requests per minute, the retry logic uses exponential backoff, and the ceiling is probably around 30 seconds.

**After**

> The client sets a 100-request-per-minute limit and retries with exponential backoff (`client.py:44`). The 30-second ceiling is my recollection of the library default, not something I checked.

Three claims in one flat voice: two verified, one recalled. The reader cannot tell which to trust, so they must discount all three. *Diagnostic: for each claim, could you name where it came from? If the sources differ, say so.*

---

## 6. Buried subject, buried news

**Before**

> The implementation of caching for the results of the expensive similarity computation, which was added in the last commit, is what causes the memory growth that you observed.

**After**

> Memory grows because last commit's similarity cache never evicts.

The subject runs nineteen words before reaching its verb, and the sentence ends on *observed* - the reader's own report, not the news. *Diagnostic: read the first eight words, then the last four. Is a real actor at the front and the point at the back?*

---

## 7. Nominalization

**Before**

> Verification of the input parameters is performed by the wrapper prior to the invocation of the solver.

**After**

> The wrapper checks the parameters before calling the solver.

Three actions hidden in nouns - *verification*, *invocation*, *performance* implied - leaving a sentence with no real verb. *Diagnostic: circle every noun ending in -tion or -ment. Each is a verb you refused to use.*

---

## 8. Signposting instead of connecting

**Before**

> As mentioned above, the parser is strict. It is important to note that the loader is not. Additionally, it should be noted that this asymmetry causes the bug described earlier.

**After**

> The parser is strict but the loader is not, and that asymmetry is the bug.

Signposts point at relationships instead of carrying them. Three words - *but*, *and*, *is* - do the work of three signposts. *Diagnostic: if you cut every reference to the document itself, do the sentences still connect? If not, fix the connection, not the signpost.*

---

## 9. Menu ending

**Before**

> The fix is committed. Let me know if you'd like me to add tests, or update the docs, or refactor the surrounding module, or check whether the same bug exists elsewhere in the codebase. I'm happy to help with any of these!

**After**

> The fix is committed. The same pattern appears in `loader.py`, and it's worth checking before this ships.

Four options make the reader do the triage you were positioned to do. Recommend one, or stop. *Diagnostic: of the next steps you listed, which would you actually do first? Say that one.*

---

## 10. Over-compression

The rules overshoot in this direction too. Both of these are failures.

**Too terse**

> Fixed. Cache eviction.

**Too padded**

> I've now gone ahead and implemented a fix for the issue you reported. The approach I took was to add an eviction policy to the caching layer, which should address the memory growth problem that you were seeing in production.

**Right**

> Fixed: the similarity cache now evicts at 500 entries, which holds memory flat across a full run.

The terse version makes the reader reconstruct the meaning; the padded version makes them wade for it. Both fail the same test from opposite sides. *Diagnostic: does every word do work, and can the reader stop after one pass?*

---

## 11. A list wearing prose

**Before**

> A skill at `~/.claude/skills/prose-style` holding three files: `SKILL.md` with the governing rule, reply-shape rules, a revision checklist, and a named list of my worst habits; `references/general.md`, a single rulebook organized by the order decisions arise - stance, shape, order, words, rhythm - blending five guides; and `references/examples.md`, ten before-and-after pairs, each with a diagnostic.

**After**

> Three files. `SKILL.md` - the governing rule, reply shape, revision checklist. `references/general.md` - the rulebook, organized by decision order. `references/examples.md` - before-and-after pairs with diagnostics.

Three items of equal weight, crammed into sixty words with semicolons and no working verb. This is "prefer prose to bullets" applied past its purpose: prose carries cause and contrast, and these items share nothing but membership in a set. *Diagnostic: if the items relate only by belonging to the same set, they are a list.*

---

## 12. A count chosen for rhythm

**Before**

> The content changed shape three times. Strunk was demoted from the frame. Rule 17's limit clause went in. Your two corrections restructured the overrides. Finally the register split collapsed.

**After**

> The content changed shape four times.

The number came from the cadence of the sentence, not from the items after it. Announced counts are the one claim in a draft that can be checked mechanically, so there is no excuse for getting one wrong. *Diagnostic: if you announce a number, count what follows.*

---

## 13. The actor erased from shared work

**Before**

> The per-source files were folded into one. The shape rules were moved into always-on config. Orwell's sixth rule was promoted to the top of the file.

**After**

> I folded the per-source files into one. You moved the shape rules into always-on config. Then you promoted Orwell's sixth rule to the top.

Every actor here is known and present in the conversation, and who decided what is the substance of the report. The passive is correct when nobody needs the actor; in an account of shared work, the actors are the point. *Diagnostic: in a report of joint work, can the reader tell who did which part?*

---

## 14. A checkable claim asserted flat

**Before**

> Nine commits in a git repo here.

**After**

> Nine commits, just counted.

The number was right, but it was written in the same voice as facts confirmed moments earlier, and nothing distinguished the two. Marking is cheap: three words separate a checked claim from a remembered one. *Diagnostic: for any number or name in the draft, did you read it, run it, or recall it? If the answers differ across the sentence, say so.*

---

## 15. The verdict last

**Before**

> I ran it on my own reply from earlier in this session. It predates every version of the rulebook, so it is a fair specimen.
>
> [six paragraphs of findings, then the revision]
>
> **What the test says about the instrument.** The procedure caught real defects and produced no false alarms, which is the result I wanted.

**After**

> The procedure works: it caught real defects in a reply written before the rulebook existed, and it raised no false alarms. It was useless against that reply's worst problem, which was architectural.
>
> [then the findings and the revision]

Showing the work before the conclusion feels rigorous, and that is why this failure survives revision - it reads as thoroughness rather than as delay. But a test report answers a question, and the answer is the verdict. Evidence supports a conclusion the reader already holds; it does not build one they are made to wait for.

The same shape appears in review findings, benchmark results, debugging reports, and any reply that ends with "so the answer is." *Diagnostic: find the sentence that answers the question. If it is not in the first paragraph, move it there.*

---

## 16. Restating the artifact you just wrote

**Before**

> Committed as `5f27975`. Fifteen pairs, counted from the file.
>
> Pair 15 covers the shape rather than the single instance: a report that shows its work before its verdict. The note explains why this one survives revision - delaying the conclusion reads as thoroughness, so it never feels like a defect - and generalizes it to review findings, benchmarks, and debugging reports.
>
> `SKILL.md` now says fifteen where it said fourteen.

**After**

> Added as pair 15, committed `5f27975`.

The user asked for a mechanical edit and received three paragraphs paraphrasing a file they can open. This is the file-writing form of narrating tool calls: the artifact exists, so describing it adds a second, worse copy.

Report what the reader cannot see - a decision you made, a failure, a surprise. Never re-tell the content of a file you just wrote. *Diagnostic: could the reader learn this by opening the file? Then cut it.*

---

## 17. Performing compliance

**Before**

> Fifteen pairs, counted from the file. I checked the first eight words of each sentence and varied the lengths, so the passage should read cleanly now.

**After**

> Fifteen pairs.

Announcing that you ran a check is metadiscourse about your own process, not information. The check shows in the prose or it did not work. A reader wants the count, not evidence of your diligence in obtaining it.

The exception is evidence marking, which is not the same thing. *From memory, so check* changes how much weight a claim carries. *Counted from the file* only advertises that a rule was followed. *Diagnostic: does the note change what the reader should believe, or only what they should think of you?*

---

## Adding to this file

When a reply reads badly, save it. Write the revision beside it, name the failure, and state the diagnostic in one sentence. An example drawn from a real reply is worth more than an invented one, because the invented failure is always a little too obvious.
