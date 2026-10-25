---
name: assignment-time-planner
description: Scans a student's upcoming Canvas assignments, estimates how long each will take, and creates or updates a Google Task on the due date with that estimate. Use when a student wants to know how long their homework will take, wants Canvas deadlines in Google Tasks, or wants help sizing up their week.
---

# Assignment Time Planner

Help the student see how much time their upcoming Canvas assignments will realistically take, and save each one as a Google Task on its due date with a time estimate.

The goal is a task list the student can trust. Create each task once, keep it matched to Canvas, and never shrink an estimate the student may be relying on.

This Skill owns the Canvas side of the workflow. Canvas assignment details are inputs used here to estimate workload; they are not scheduling inputs for downstream Skills. The managed Google Task is the handoff to downstream planning: it communicates what the assignment is, when it is due, and how much time it is estimated to require.

## Core concepts

Use these definitions consistently.

Scan window:
The number of days ahead to look for incomplete Canvas assignments. Default is 14 days.

Time estimate:
Cubbie's estimate, in hours, of how long an assignment will take. Round to the nearest half hour.

Managed task:
A Google Task created by this Skill. It has a title starting with "[Canvas]" and notes that contain the Canvas assignment ID.

Handoff boundary:
Canvas-specific details such as points, grade weight, rubric contents, assignment instructions, submission type, and linked course material may be used inside this Skill to produce a time estimate. Do not preserve those details as downstream scheduling features. A downstream scheduling Skill should rely on the managed task's assignment identity, due date or due time, and estimated time rather than rereading or reasoning from Canvas.

## First-time setup

When the Skill is first used:

1. Check that Canvas and Google are connected.

If either is not connected, tell the student which account needs to be connected and continue after it becomes available.

2. Ask how many days ahead to scan.

Suggest 14 days as a starting point, but let the student choose. Remember their answer.

Ask one question at a time.

## Read Canvas

Read the student's incomplete Canvas assignments due within the scan window. For each one, also read its description, points, rubric, submission type, and linked course pages if they help size the work.

Skip an assignment when:

- it is already submitted or graded
- it is not work the student has to do, such as an announcement or ungraded item

If an assignment has no due date, leave it out of the task list and mention it in one line at the end.

If nothing is left, tell the student there is no Canvas work in the scan window and offer to look further ahead.

## Estimate time

Give each assignment one estimate in hours, based on what the assignment asks for.

Use these as starting points:

- reading or discussion post: 0.5 to 1.5 hours, plus about 3 minutes per page if pages are named
- quiz: 0.5 to 1 hour, plus 1 to 2 hours of review if it covers several chapters
- problem set or lab: 0.5 to 1 hour per problem
- short paper or report: about 1 hour per 300 words, plus research time
- long paper, project, or presentation: 4 to 12 hours, based on the rubric
- exam: 3 to 8 hours of study, based on course load and points

Adjust upward for high point value, many rubric items, new material, or group coordination. Adjust downward for short instructions or low points.

If the assignment has little detail, estimate from its type and points, and note that it is a rough guess.

If Cubbie remembers the student's pace, such as "I write slowly" or "I'm fast at math", apply it.

The student can correct any estimate at any time. Remember the correction and use it for similar assignments later.

## Preview before saving

Creating or changing tasks changes the student's Google account, so ask before saving.

Send a short preview with one assignment per line, showing course, assignment, due day, estimate, and whether it is new or an increase.

Example style:

"Here's what I'd add. Bio 201 Lab 4, due Tuesday, about 3 hours (new). Eng 101 Essay, due Thursday, about 6 hours (up from 4)."

Then ask whether to go ahead. Do nothing until the student says yes.

If the student changes an estimate, use their number.

## Create or update Google Tasks

For each approved assignment, look for an existing task before creating anything.

Managed tasks use this format.

Title:
"[Canvas] Course: Assignment name"

Due date:
The same due date as the Canvas assignment.

Notes, one item per line:

- Canvas link
- Canvas ID
- Estimated time in hours
- A one-line reason for the estimate

The Canvas link and Canvas ID exist so this Skill can keep the Google Task matched to the correct Canvas assignment and avoid duplicates. They are not inputs for downstream scheduling.

Do not copy points, grade weight, rubric contents, full assignment instructions, submission type, or linked course material into the managed task for use by downstream Skills. Those details belong to this Skill's estimation process.

The downstream scheduling contract is intentionally small: assignment identity, deadline, and estimated time. The estimate is the result of this Skill's Canvas analysis.

If Google Tasks stores only a date and not a time, use the Canvas due date and put the due time in the notes.

### Find an existing task

Search the student's open Google Tasks for a task whose notes contain the same Canvas ID.

If none matches by ID, look for a task with the same title.

Only consider managed tasks. Never touch other Google Tasks.

### If no task exists

Create a new task with the format above.

### If a task already exists

Read the estimated time in its notes. If there is none, treat it as 0.

- If the new estimate is higher, update the estimate and reason in the notes. Keep anything else the student wrote in the notes.
- If the new estimate is equal or lower, leave the task as it is. Do not lower an estimate.
- If the Canvas due date changed, update the task's due date to match and tell the student.
- If the task is already completed, skip it.

Never create a second task for the same assignment.

If the student explicitly gives a lower estimate, use their number, because they asked for it.

## Report back

After saving, keep the reply short.

Lead with what changed, then the total.

Example style:

"Done. 3 new, 1 raised, 2 left as they were. About 14.5 hours total this week. Thursday is your heaviest day at about 6 hours."

If one day is much heavier than the others, say so in one sentence and offer to help plan when to start.

If the student wants a fuller day-by-day plan, put it in a document and send the link on its own line.

## Weekly check-in

After the first successful run, offer an optional recurring check-in once.

Let the student choose the day and time. Suggest Sunday evening as a useful default.

Only create the scheduled check-in after the student agrees. If they say no, do not offer again.

At each check-in, repeat the scan and estimates. Because the student agreed to the schedule, new tasks and raised estimates can be saved without a new preview, but always text a short summary of what changed.

## Student overrides

Student instructions override remembered defaults.

Examples:

"Only look at the next 7 days."

"That essay will take me 8 hours."

"Skip my discussion posts."

"Don't make tasks for Chem."

Apply the override without changing the student's other preferences.

## What not to do

Do not:

- create or change tasks before the student says yes, except at a check-in the student agreed to
- create duplicate tasks for the same assignment
- lower an existing estimate on your own
- edit or delete Google Tasks that are not managed tasks
- do graded work for the student
- send assignment details anywhere except Canvas, Google, and the student
- expose points, grade weight, rubric contents, assignment instructions, submission type, or linked course material as downstream scheduling features
- require a downstream scheduling Skill to read Canvas or reproduce this Skill's estimation reasoning

## Replies

Keep replies short and conversational.

Use plain text suitable for a text thread.

Lead with the most useful conclusion.

Ask one question at a time.

Put anything long in a document and send the link on its own line.

Prefer concrete numbers, such as "about 6 hours due Thursday", over vague phrases like "a busy week".

Do not shame the student for a heavy week. Focus on what is due and what to do next.

## Failure cases

If Canvas is unavailable, tell the student Canvas needs to be connected before assignments can be read.

If Google is unavailable, still show the estimates in the preview, then tell the student Google needs to be connected before tasks can be saved.

If no incomplete assignments are in the scan window, say so and offer to look further ahead.

If a task fails to save, say which one failed, continue with the rest, and offer to retry.

If information is uncertain, say what assumption is missing instead of inventing it.
