# Sprint 2 Report (October 6–November 2, 2026)

## YouTube Link for the Sprint 2 Video

https://youtu.be/0yQx_yXZ9Yc

## What's New (User Facing)

- Draw and erase freehand marks, add lines and shapes, and enter or edit text on the canvas. Undo and redo edits while working.
- Find shapes by name or category, and upload pictures to a reusable library for placement on the canvas.
- Move, resize, recolor, or rotate canvas objects. Use box selection to move several objects together and undo the move in one step.
- Save an editable drawing and reopen it from the Drawing library with its undo and redo history intact.
- In the teacher demo, configure available tools and assignment requirements, or open a saved drawing in View only and step through its edit history.

The team included the box selection updates in the Sprint 2 deliverables. The final commits for that feature landed on November 7, after the reporting period.

## Work Summary (Developer Facing)

We built the canvas in React and TypeScript with React-Konva and connected it to a Django backend. One of our main design challenges was deciding what the database should store. We represented the current canvas as individual drawing objects and kept an ordered journal of edits so the same saved drawing could support both continued editing and playback. We used a database transaction to keep the current scene and its journal in sync during a save.

## Unfinished Work

A couple of Free Draw features are still in the process of being implemented. We plan to continue that work in the next sprint.

- Drawing saving and playback - Drawings should be able to saved and reopened. Teachers and students should be able to view the playback of the image being drawn step by step. 
- Image bank - We will work to create an image bank where students will be able to look up specific images to use in their drawing. 
- Teacher page - Currently, the teacher settings are just a tab on the drawing tool. In the next sprint we will work to implement a full teacher settings page seperate from the student view. 

## Completed Issues/User Stories

Sprint 2 tracks these stories by ID in this report. The status reflects what the standalone Free Draw prototype supports.

| ID | User story | Sprint 2 outcome |
| --- | --- | --- |
| US-03 | As a student, I want to draw freehand and adjust options such as color or line width when available so that I can show relationships and distinguish parts of my drawing. | The pen supports freehand drawing, with color and pen width controls when enabled. |
| US-04 | As a student, I want to erase marks, undo or redo changes, and confirm before clearing my drawing so that I can revise my work without accidentally losing it. | Complete per team confirmation. |
| US-05 | As a student, I want to add, edit, and position labels when text tools are enabled so that I can explain what parts of my drawing represent. | Students can add and edit text boxes and move them when the activity settings allow it. |
| US-06 | As a student, I want to save my drawing and see whether the save succeeded so that I can pause my work and return to it later. | The canvas reports save success or failure. Saved drawings can be reopened from the Drawing library. |
| US-08 | As a student, I want to reopen a saved drawing or revise a submitted drawing when the activity allows it so that I can continue or correct my work. | Complete per team confirmation. |

Related implementation records from the local Git history include the [picture library and text box update (PR #3)](https://github.com/KhoaTa06/WSU-GROUP-COORD-Free-Draw/pull/3), [shape rendering and toolbar fixes (PR #4)](https://github.com/KhoaTa06/WSU-GROUP-COORD-Free-Draw/pull/4), and [drawing API, UI, and shape selection work (PR #5)](https://github.com/KhoaTa06/WSU-GROUP-COORD-Free-Draw/pull/5).

## Incomplete Issues/User Stories

| ID | User story | Sprint 2 status |
| --- | --- | --- |
| US-01 | As a teacher, I want to enable drawing responses, write instructions, and choose which supported tools students can use so that the response format fits the activity. | **Partial.** Teacher settings support instructions and tool selection in the prototype. Enabling drawing as a response type in a classroom activity remains open. |
| US-02 | As a student, I want to see the question, drawing instructions, and available tools when I open an activity so that I know how to begin my response. | **Partial.** The standalone canvas shows a title, instructions, and available tools. Opening it from an activity with the activity's question remains open. |
| US-07 | As a student, I want to preview and submit my drawing and receive confirmation so that I know what I turned in and whether it was received. | **Partial.** The submission check shows whether the drawing meets the configured requirements and offers a JSON download. A submission preview, classroom turn-in, and receipt confirmation remain open. |
| US-09 | As a teacher, I want to open a submitted drawing from the correct student and activity so that I can review the visual response. | **Partial.** The View only demo opens saved drawings and plays back edits. Finding a submission by student and activity remains open. |
| US-10 | As a student or teacher, I want the drawing workspace or submission view to be usable on supported classroom devices so that I can complete or review the activity on the device available to me. | **Unverified.** The supported classroom devices and validation results were not confirmed. |

## Code Files for Review

- [useDrawing.ts](https://github.com/KhoaTa06/WSU-GROUP-COORD-Free-Draw/blob/0cd958e1732e41573eaba8e8906a5fab5ff1755e/freeDraw/src/drawing/useDrawing.ts) — Canvas editing, selection, and undo and redo.
- [useDrawingStorage.ts](https://github.com/KhoaTa06/WSU-GROUP-COORD-Free-Draw/blob/0cd958e1732e41573eaba8e8906a5fab5ff1755e/freeDraw/src/drawing/useDrawingStorage.ts) — Frontend save and reopen flow.
- [canvas_storage.py](https://github.com/KhoaTa06/WSU-GROUP-COORD-Free-Draw/blob/0cd958e1732e41573eaba8e8906a5fab5ff1755e/backend/api/canvas_storage.py) — Backend storage for editable drawings and action history.

## Retrospective Summary

- **What went well** — We got better at thinking through how elementary school students would interact with the tools and at communicating with our client.
- **What we want to improve** — We want to improve the teacher page with more features and a seperate interface.
- **Changes planned for the next sprint** — Continue implementing the remaining Free Draw features.
