# Prototype · Juno

The assumption the prototype tests is that the initiative name is a reliable enough key to connect Notion, Linear, Zentrik and Teams, so one name can produce a single picture a PM can act on without opening each tool.

## Prototype link

https://claude.ai/artifact/SXVMCZM7R1YukW9eRHzhnD

_____

## What it demonstrates

It demonstrates one flow: a PM types an initiative name and gets back a documentation scorecard where every requirement has a result and a named item behind it, and a tool failure never looks like a failed requirement.

In the prototype that plays out as:

The PM enters a name, or a short form like “appt reminders” or “intake”, and Juno resolves it to one initiative.
Juno shows a search of Notion, Linear, Zentrik and Teams one tool at a time, with a result for each.
Juno shows a report: a bottom line calculated from the rows, a name check per tool, the nine-row scorecard, gaps, open questions, sources and confidence.

_____

## Debrief

What broke

Stale items are not a first-class concept. Your task asks Juno to surface stale items, but the prototype only catches one by accident. The L5 gap (latest Pulse is 13 days before the end of the reporting week) is labeled Not found. Other old dates, like the Intent Canvas last edited 2026-10-08, are shown but never flagged. You need a staleness rule (for example, an age threshold per source type) and a visible Stale label.
Conflicts between tools are untested. None of the three scenarios has two tools disagreeing. The Teams mention is deliberately context only, so it doesn’t count. The “synthesize across tools” part of the task has no scenario that exercises it.
Traceability is incomplete. Scorecard rows name their evidence, but the bottom-line sentence, the gap bullets, the open questions and the confidence reason don’t point to a specific source. That falls short of “every statement must trace back to a source.” The scorecard links are also placeholders, so nothing is clickable yet.

What held up (by design, not by test)

Separating Not met, Not found and Can’t verify, so a tool failure never reads as a failure of the initiative.
Treating the name match as a flagged, unconfirmed dependency that lowers confidence (the Appointment Reminders v2 case).
Showing Above range as a count rather than a failure.
