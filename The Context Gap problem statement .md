# The Context Gap

**A problem statement for a call context layer**

---

## The essence

We hold every conversation we need in order to run our engagements well, and we retain almost none of it in a form anyone can act on.

Decisions, client commitments, constraints and warnings are spoken once, captured into a transcript, and then functionally lost. What remains is a folder of files that only a human can read, one at a time, slowly. The consequence is that we re-ask questions we have already answered, miss commitments we made out loud, and cannot demonstrate to a client what we have learned from our other clients.

This is not a discipline problem and it is not solved by people trying harder. It is a systems problem: nothing in our current chain accumulates.

---

## 1\. What this is not

Worth being precise, because the obvious reading of this problem leads directly to the wrong solution.

**This is not a transcription problem.** We already have transcripts.

**This is not a summarisation problem.** Note-taking tools already summarise. Every one of them produces a tidy recap with action items at the end of a call. That capability has been available to us throughout and it has not closed the gap.

The reason is that a summary is bounded by a single meeting. It cannot know that the commitment made on this call is the same commitment made three weeks earlier and still unfulfilled. It cannot know that what was agreed with the client on Tuesday was quietly contradicted internally on Thursday. It cannot know that this is the fifth time the client has asked for the same report.

**The problem is that context does not accumulate.** Thirty excellent summaries are still thirty disconnected documents. What is needed is a single evolving picture of each engagement, where each new call updates a state rather than adding a file.

---

## 2\. How work happens today

1. A call occurs.  
2. A note-taker produces a transcript.  
3. The transcript lands in a notes tool and is copied into a folder.  
4. A human reads it, forms a view, and sometimes writes the resulting commitments into a tracker.  
5. That tracker is the only consolidated record of what we owe anyone.

Steps 4 and 5 are manual. They compete directly with delivery work, and they lose every time. Nothing in the chain fails loudly when it breaks.

---

## 3\. The four failures

### 3.1 Knowledge dies in the transcript

A single active engagement accumulated more than thirty transcripts across roughly seven weeks, amounting to several hundred thousand words of conversation. Answering a question as basic as *"what exactly did we promise about reporting, and on what date"* requires opening files and reading them.

Nobody does this at the frequency the work demands. So decisions get made without the context that already exists in the building.

### 3.2 Commitments decay silently

The commitment tracker is maintained by hand and sourced from call transcripts. In the case that prompted this document, it went **47 days without an update** while the engagement continued at full pace.

It still listed more than a dozen open items, several marked "not started", including one annotated as blocking an entire reporting workstream. Nobody could say which of them were still open, because finding out meant re-reading seven weeks of transcripts.

A stale tracker is not a neutral state. It is worse than no tracker, because people stop trusting it, then stop looking at it, and the commitments inside it stop existing in any practical form at all.

### 3.3 Internal and external context cannot safely coexist

Internal calls contain our candid assessment of an engagement: what is actually going wrong, what we think of the brief, where we are behind, what we are not saying out loud. Client calls contain what we formally committed to.

Today these sit in the same place with no boundary between them. That single fact has blocked automation entirely. Any system built on top of that store risks surfacing internal commentary in a client-facing output, and the cost of that happening once is severe enough that the rational response has been to automate nothing.

So the separation is not a feature of the solution. It is the precondition for there being a solution at all.

### 3.4 There is no memory across clients

This one tends to arrive as direct criticism from the client. A representative example, recorded verbatim with the firm's name redacted:

We do have the learnings. They sit in transcripts, in folders, organised per client, unreadable at any scale beyond one person reading one file. Because we cannot retrieve across engagements, we present to the client as an organisation that has learned nothing from its other work.

The knowledge existing and the retrieval not existing are, from the outside, indistinguishable situations.

---

## 4\. The nuances that make this hard

These are the reasons an off-the-shelf tool has not already solved it.

### 4.1 The two contexts must be separate and related at the same time

Both naive solutions fail.

**Merge them**, and internal candour leaks into client-facing output. Unacceptable, and the risk alone is enough to stop anyone switching the system on.

**Keep them wholly apart**, and you lose the most valuable insight in the entire system, because that insight lives exactly at the join. A client asking for the same thing for the fifth day running is one fact. The internal blocker that makes producing it impossible is a second fact. Neither is interesting alone. Together they are the single most actionable thing anyone could surface that week.

What is required is **relation without merger**: the ability to link an internal fact to an external one and traverse that link, without the text of the internal fact ever becoming copyable into something a client sees. The direction of visibility has to be asymmetric, and it has to be enforced by the structure of the data rather than by anyone remembering to be careful.

### 4.2 The signal is noisy, and unevenly so

The two classes of call have very different transcript quality.

Client calls are typically clean: named participants, one language, reasonably structured. Internal calls often are not. They are faster, they overlap, they are frequently code-switched between languages, and speaker labels degrade to generic markers. Code-switched speech raises word error rate by 30 to 50 percent over monolingual speech, and it shows.

So the system cannot apply one extraction standard uniformly across both. It needs a repair step for the noisy class. More importantly, it needs every claim it makes to be traceable to a verbatim quote from the source, so that a garbled input produces a flagged low-confidence item rather than a confidently wrong one.

### 4.3 Being confidently wrong is worse than being silent

A tracker that fills with plausible but incorrect tasks will be abandoned faster than a stale one, and it is harder to recover from, because it poisons the trust that any future version depends on.

This is why the system must propose rather than impose, at least until its accuracy is demonstrated rather than assumed. The cost of a missed item is that we are exactly where we already are. The cost of a fabricated item is that nobody uses the system again.

### 4.4 Silent failure is the actual enemy

Part of this has already been attempted. A scheduled job was written to pull meeting notes automatically on a daily cadence.

It never completed a single successful run. It was blocked by a permissions error on the machine it ran on, it logged that error to a file nobody read, and it stayed broken for roughly two months without anyone noticing.

This is the most instructive fact available to us. The failure was not that the automation was hard to write. It was written. The failure was that it ran on a local machine that had to be awake, and no part of the system knew it was supposed to have run.

Any solution must therefore run on infrastructure that does not depend on an individual's laptop, and must raise an alarm when it has not run. **A system that fails silently is worse than no system, because it manufactures false confidence.**

### 4.5 One store, many surfaces

There is a strong temptation to pick a task tracker and make it the home of all this. That is a trap.

The moment the tracker is the source of truth, the system is welded to that vendor's API, there is nowhere to keep evidence and confidence scores alongside each item, and cross-client retrieval becomes impossible because the data model belongs to someone else.

The context has to live in one store that we control. Every tracker, document and digest is then a rendered view of it. This is also the only reading of *"everything stored in one place"* that survives contact with a second client.

---

## 5\. What the status quo costs

Clients tend to quantify this for us without being asked. Representative, verbatim, anonymised:

*"This is the fifth day when I'm asking for data of what's happening with the campaigns."*

*"It took us three days to activate a campaign. Come on."*

*"Every hurdle that we faced should have been preverified."*

*"We are investing too much time going back and forth on confirming from our end whether we should do this or should not do this."*

And the structural version of the complaint, as it was eventually written down internally:

The relationship complaint is not about any single piece of work. It is that we have been asking the client what to do rather than proposing what to do, and that execution has been slower than promised.

That sentence is the business case. **Proposing requires synthesis across everything already discussed.** Synthesis is exactly what is impossible when the discussion is trapped in dozens of separate files. The behaviour the client is asking for is downstream of a capability we do not currently have.

There is also an asymmetry worth naming plainly: **the client remembers what we promised them, and we do not.** Every meeting where that gap becomes visible costs credibility that is expensive to rebuild.

---

## 6\. What a solution must do

Stated as requirements, deliberately not as design.

1. **Ingest automatically.** Transcripts arrive without a human moving a file.  
2. **Accumulate rather than summarise.** Each call is reconciled against everything said before, producing a current state of the engagement. The system must recognise when a new statement supersedes, contradicts, duplicates or fulfils an earlier one.  
3. **Separate internal and external context by construction.** Internal context may draw on client context. Client-facing output must never expose internal context. Enforced structurally, not by prompt instruction and not by care.  
4. **Relate the two without merging them.** Link a client's repeated request to the internal blocker behind it, because the link is where the value is.  
5. **Ground every claim in a verbatim quote.** Anything the system asserts must be traceable to source text. Anything it cannot verify is flagged for review, never published and never silently dropped.  
6. **Propose, do not impose.** Output is a draft for human approval.  
7. **Work across clients from day one.** Cross-engagement retrieval is a stated client expectation, not a future nice-to-have, and retrofitting multi-tenancy later is expensive.  
8. **Fail loudly.** Every scheduled component reports that it ran. Absence of a report is an alert.  
   ---

   ## 7\. What success looks like

Measurable, so we can tell whether this worked.

* The commitment tracker is never more than one business day stale, with nobody maintaining it by hand.  
* Within an hour of a call ending, the owner has a draft list of what was committed, by whom, with the quote that proves it.  
* *"What have we learned about this across our clients"* becomes a query rather than a research project.  
* A repeated client request is detected on its second occurrence, not its fifth.  
* Contradictions between what we told a client and what we said internally surface within a day.  
  ---

  ## 8\. Scope and non-goals

**In scope:** ingestion, the persistent per-client context layer, extraction with evidence, reconciliation against prior context, proposed actions, and scheduled nudges. Multi-client from the outset.

**Explicitly not in scope:** replacing human judgment on what to do, sending anything to a client automatically, or taking any action without approval.

---

