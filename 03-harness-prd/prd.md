# Harness Sketch

Describe Juno's role and task: You are Juno, an Associate PM embedded in a product team. You work across the team's connected tools (for example Linear, Notion, Zentrik, Fireflies, and Teams) to help PMs keep track of documentation that is scattered across them. You support PMs; you do not own product decisions. You read, connect, and summarize. You never create, edit, delete, or send anything in any tool on your own, and you never set priorities or make commitments on the team's behalf.

_Rough first pass, Module 3 Lab 1. Not the AI PRD._

## 01 · Context
What it gets to see
For any initiative it’s looking at, Juno sees the Intent Canvas in Notion, the Linear initiative with its project and milestones, the Zentrik studies and interviews, the Fireflies transcripts, and the Teams conversation. It also gets the team standard as a checklist so it knows what “done” looks like. It pulls these in one initiative at a time rather than loading everything. It doesn’t see other PMs’ initiatives unless asked, and it works from transcript summaries instead of the raw text.

What it’s allowed to do

On its own: read everything, compare it against the standard, and create a missing Linear or Zentrik initiative using the exact name from Notion.
After checking with the PM: write milestones, attach Fireflies transcripts, and nudge anyone on Teams.
Never: delete anything, rename existing records, or edit a PM’s Intent Canvas. When it hits something ambiguous, like two possible matches, it stops and flags it to the PM.

What persists across sessions
Juno keeps a ledger per initiative: when it last checked, what it created, and what it flagged and hasn’t been resolved yet. That lets it pick up where it left off rather than re-auditing from scratch. Only Juno writes to it. It resets weekly, in line with the Linear Pulse cadence, so old state doesn’t linger. Anything it learned about a PM’s preferences would live outside the ledger and only change when the PM says so.

## 02 · Tools
Attempts: how many tries before it hands back

Per action: 2 attempts. If a write fails or the re-read doesn’t confirm it, Juno tries once more and then stops. A third try is just guessing.
Per initiative per sync: at most 5 actions in total, so one messy initiative can’t turn into a runaway session.
Stop signals: any ambiguity (two possible matches, a name that almost matches), a verification failure after the retry, or a tool error that repeats. In each case it writes a flag in the report naming what it tried and what it needs from the PM, then moves to the next initiative.

Permissions: tiered by how much damage a wrong action could do

Tier	Juno’s actions	Why
Free (no asking)	Read in any of the five systems. Create a missing Linear or Zentrik initiative with the exact Notion name. Update its own ledger.	Reads can’t hurt anything. A new initiative is easy to spot and easy for a PM to delete.
Ask first	Write Linear milestones. Attach Fireflies transcripts. Link an existing record to an initiative. Send any Teams message.	These change records PMs already own, or they reach other people.
Never	Delete anything. Rename existing records. Edit a PM’s Intent Canvas. Change dates or statuses.	The damage is hard to undo, and it’s the PM’s judgment call.

## 03 · Loop
Loop: how many times may it try?

Attempt budget
- Per action: 2 attempts (the original try plus one retry). A retry only happens after a specific, fixable failure, such as a timeout or a re-read that hadn't caught up. It is never a blind repeat.
- Per initiative, per sync: at most 5 write actions total.
- Per run: one pass over each initiative in scope. Juno does not loop back to an initiative it already handed off.

What tells it to stop (any one is enough)
- Verification fails after the retry (the re-read doesn't show the record, the name doesn't match exactly, or the link doesn't resolve).
- Ambiguity: two possible matches, a name that almost matches, or a record that looks like a duplicate.
- The same tool error twice in a row.
- The next step would be a confirm-tier or blocked action and no PM approval is available.
- The 5-action budget for that initiative is used up.

What it does when it stops
- Marks the item as flagged, never complete.
- Writes to the report: what it tried, what it saw, and what it needs from the PM.
- Records the flag in its ledger so the next sync doesn't repeat the same attempt.
- Moves on to the next initiative. One stuck initiative never blocks the others.

Justification
- 2 attempts per action: the first failure is often transient, but a third try on the same action is guessing and risks duplicate records across Linear and Zentrik.
- 5 actions per initiative: a normal gap closure (initiative, project link, transcript attach, and so on) fits well within it. A pattern that exceeds it likely means something is wrong that a PM should look at, not that Juno needs more room.
- Handing back instead of retrying more: the cost of a flag is one PM glance. The cost of Juno pushing through ambiguity is a wrong record that looks authoritative.

## 04 · Memory
Memory: what survives once this ends?

What persists across sessions (per initiative)
- Sync ledger entry: last checked (date/time), what Juno created (record, system, ID), and which checklist items passed or failed at last check.
- Open flags: what Juno stopped on, what it tried, and what it needs from the PM. A flag stays open until the re-read shows it resolved.
- Pending confirms: confirm-tier actions Juno proposed that the PM hasn't approved or declined, so it doesn't re-ask or silently drop them.
- Name map: the Notion initiative name and the matching Linear and Zentrik record IDs, so the next sync finds matches by ID instead of re-guessing from names.

What expires
- Passed checklist results: weekly, in line with the Linear Pulse cadence. Juno re-verifies instead of trusting last week's pass.
- Resolved flags: dropped after one cycle, once the re-read confirms the fix.
- Declined confirms: kept for one cycle so Juno doesn't re-propose the same action, then cleared.
- Anything about an initiative that is closed or archived in Linear.

What never persists
- Raw transcript text, Intent Canvas content, or any copy of PM-owned records. Juno stores pointers (IDs and links), not content, so memory can't go stale or leak.
- Anything from the demo fixtures treated as real. Fixture data is marked as such in the ledger.

Who may write
- Only Juno writes to the ledger.
- PMs can read their own initiatives' entries and clear a flag or decline a confirm. Nobody else edits entries.
- Team-wide preferences (for example "don't nudge on Fridays") live outside the ledger and change only when you or a PM sets them explicitly. Juno never infers them.

Justification
- IDs and pointers instead of content: a stale pointer fails visibly on re-read, while stale copied content looks right and is wrong.
- Weekly expiry: it matches how often the team standard is checked, and it forces re-verification instead of letting an old pass hide a new gap.
- Juno-only writes: if PMs or other tools edit the ledger, Juno can no longer trust it as a record of what it actually did.

## 05 · Permissions
Permissions: what can it do without asking?

Allowed without asking (auto)
- Read: any of the five systems (Notion, Linear, Zentrik, Fireflies, Teams), for initiatives in scope.
- Draft: flags, proposed milestone lists, and Teams nudge text. Drafts stay inside Juno's report until a PM acts on them.
- Write, additive creates only: create a missing Linear or Zentrik initiative using the exact Notion name, and update its own ledger.
- Verify: re-read anything it just wrote and run the team standard checklist.

Needs a yes first (confirm)
- Writing Linear milestones.
- Attaching Fireflies transcripts to an initiative or to the Zentrik Morning Huddle.
- Linking an existing record to an initiative.
- Any Teams message, since it goes to people under a PM's name.

Never (blocked)
- Deleting anything.
- Renaming existing records.
- Changing statuses or dates.
- Editing a PM's Intent Canvas.

How tiers are decided
- Tiered by how much damage a wrong action could do and how easily it can be undone.
- A new record is one item in one system. It's easy to spot and easy to delete, and Juno re-reads it right after creating it.
- Touching a record a PM already owns, or reaching a person, is harder to notice or undo, so it waits for a yes.
- A confirm only covers that one action. Approving one transcript attach does not approve the next.
- If a confirm-tier action comes up and no PM is available (a scheduled or unattended run), Juno holds that step, finishes the rest, and reports what it held.

## 06 · Verification
Step 1: The change
When a PM creates an initiative in Notion, Juno creates the matching Linear and
Zentrik initiatives, with the same name, within one business day, without the PM
doing anything. Juno runs on a scheduled daily sync. Writing milestones and the
Intent Canvas stay with the PM.

Step 2: Goal metric
Two numbers, so we can tell who is driving the result.

A. Match rate (Juno-controlled)
   - % of active initiatives with a matching record in Notion, Linear and Zentrik,
     with identical names.
   - Target: 95% within one business day of the Notion initiative being created.

B. Standard rate (shared between Juno and PMs)
   - % of active initiatives meeting the documentation standard: matching names
     across all three tools, an Intent Canvas, and a Linear project with
     milestones.
   - Today without Juno: count by hand. Check every active initiative against the
     standard; that count is the baseline. If there is no audit yet, use a rough
     estimate labeled as an estimate (e.g., "about 50%, to be confirmed by a
     manual audit before launch").
   - Target: 90% within 8 weeks of rollout.

If B stalls while A is high, the gap is PM-owned work (Canvas, milestone
approvals), not Juno.

Step 3: Usage metric and pattern to watch
- Metric: % of Juno's auto-created Linear and Zentrik records kept as-is (not
  deleted, renamed, or recreated by a PM). Measured from the ledger, which stores
  the ID of every record Juno creates.
- First pattern to watch: PMs deleting or renaming Juno's records. That means
  Juno is creating clutter or wrong names, so it is saving no work and may be
  adding some.
- Also watch: confirm-tier requests that PMs decline or ignore (milestones,
  transcript attaches). That signals Juno is proposing the wrong things.

Step 4: Review date and stop line
- Review date: Thursday, January 14, 2027, at the end of week 8 after a kickoff
  the week of November 23. Plan around the holiday weeks. If rollout slips,
  the review date moves with it.
- Stop line: stop using Juno (or pause and fix it) if either is true by the
  review date:
  - Fewer than 60% of its auto-created records are kept as-is.
  - More than 1 in 4 of its auto-created records were deleted or renamed by PMs.
- At the review, also ask each PM two questions: did Juno save you time, and did
  you spend time fixing its records? That covers the time-spent question without
  needing new instrumentation.

Before kickoff
- Run the manual baseline audit for Metric B.
- Switch from the demo fixtures to live connections.
