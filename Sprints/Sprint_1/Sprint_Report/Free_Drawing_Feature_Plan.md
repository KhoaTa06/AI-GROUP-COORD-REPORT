# Free-Drawing Feature Plan

- Status: Planning proposal; not implemented.
- Scope: Requirements and design questions for a future free-drawing capability in the AI Group Coordinator application.
- Source: Sprint 1 planning brief. Confirm with the client before treating proposals as approved requirements.

## Problem and intended outcome

[TODO: Confirm the user problem.] Initial planning assumption: users may need to sketch or annotate an idea while coordinating group work. The feature should let a user create a freehand sketch in the relevant workflow without implying that the sketch is analyzed by AI or shared live.

## Proposed user flow

1. User opens the relevant group/task/workspace (exact parent object to confirm).
2. User selects a labeled **Free draw** toolbar action.
3. The drawing surface enters free-draw mode and accepts pointer or touch input.
4. User creates one or more strokes.
5. User can finish, cancel, or leave drawing mode. Whether undo, redo, erasing, color, and width controls are required remains open.
6. If persistence is approved, the user saves or the application autosaves according to a defined policy.
7. If collaboration is approved, the application communicates strokes to authorized participants in real time.

## Initial functional requirements to validate

| ID | Proposed requirement | Acceptance evidence to define |
|---|---|---|
| FD-01 | The user can enter and exit free-draw mode. | [TODO: Verify tool state and keyboard/touch interaction.] |
| FD-02 | The user can draw a freehand stroke using supported input devices. | [TODO: Define supported browsers/devices and acceptable stroke quality.] |
| FD-03 | The toolbar action has an understandable icon and accessible name. | [TODO: Design review and accessibility review.] |
| FD-04 | The drawing surface handles resize and supported zoom behavior without losing stroke alignment. | [TODO: Define expected resize/zoom behavior.] |
| FD-05 | Save, load, edit, export, and delete behavior follows an approved persistence policy. | [TODO: Confirm whether these are in scope.] |
| FD-06 | If live collaboration is required, only authorized participants receive drawing updates. | [TODO: Define collaboration, ordering, conflict, and reconnect behavior.] |

These are candidate requirements, not client-approved commitments.

## Konva and icon responsibilities

- **Konva / react-konva:** Candidate canvas scene graph and freehand rendering approach for the React frontend. The implementation team should assess pointer events, touch behavior, resizing, accessibility, and performance with representative drawings.
- **Icon:** A separate toolbar asset that communicates the free-draw action. A pencil/pen symbol is a proposal. Use a design-system-approved icon package or custom SVG after the team confirms the source.
- **Radix UI:** Could provide accessible UI primitives around the tool controls; it does not itself define the drawing behavior or establish which icon package is in use.
- **Tailwind CSS:** Could style the toolbar and surrounding layout within the planned frontend stack.
- **TypeScript:** Could describe tool state and the drawing payload once persistence and API boundaries are agreed.

No package selection beyond the user-provided stack is final, and no performance or compatibility testing has been performed.

## Candidate data and API questions

Before implementation, decide whether to store vector stroke data or rendered images, what metadata is needed, and which application object owns each drawing. If PostgreSQL is used for persistence, the backend team should select a schema and retention strategy. Do not assume a specific JSON shape, endpoint, or database field until requirements are confirmed.

Potential API responsibilities (names and payloads intentionally unspecified):

- Create or save a drawing.
- Retrieve a drawing for an authorized user.
- Update or delete a drawing if editing is permitted.
- Validate ownership and group/task membership on every operation.

## Real-time collaboration

Django Channels and Daphne are part of the planned stack, but their inclusion does not mean the drawing feature must be collaborative. If simultaneous shared drawing is required, define authorization, message format, stroke ordering, reconnect behavior, and conflict handling before estimating it. Otherwise, exclude real-time synchronization from the initial feature scope.

## Security, privacy, and accessibility questions

- Apply the same access policy as the parent group/task/workspace.
- Confirm whether drawings may contain personal or sensitive information and define retention/deletion behavior.
- Do not send drawings to Azure OpenAI or another model unless the client explicitly approves that use and its privacy requirements.
- Provide an accessible name, focus behavior, keyboard-operable controls, and a non-canvas way to understand or operate key actions where feasible.
- Define touch targets and supported pointer devices.

## Open decisions

- Exact user workflow and parent object.
- Icon library and approved symbol.
- Required drawing controls for the initial release.
- Save/autosave policy and ownership model.
- Individual versus shared drawing.
- Whether drawings connect to any AI functionality.
- Browser/device support, accessibility criteria, and performance expectations.

## Next steps

1. Review this proposal with the client and record approved requirements.
2. Obtain any existing repository, product brief, designs, and implementation handoff.
3. Confirm technology versions and whether Konva/react-konva fits the expected UX.
4. Decide persistence, authorization, and collaboration scope before implementation planning.
