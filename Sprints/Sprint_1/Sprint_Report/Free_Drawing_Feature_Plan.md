# Free-Drawing Feature Plan

- Status: Planning proposal updated with client direction; not implemented.
- Scope: Requirements and design questions for a future free-drawing capability in the AI Group Coordinator application.
- Current input scope: Laptop trackpad or mouse. iPad and Apple Pencil support is deferred.
- Client direction: Capture drawing coordinates during drawing and save the vector data when the student finishes; do not save an image snapshot every 15 seconds.

## Problem and intended outcome

[TODO: Confirm the exact student workflow.] Initial planning assumption: students need to sketch or annotate an idea while coordinating group work. A drawing is represented as strokes and their coordinates so it can be reconstructed later. The plan does not assume that drawings are analyzed by AI or shared live.

## Proposed user flow

1. The student opens the relevant group, task, or workspace (the parent object still needs confirmation).
2. The student selects a labeled **Free draw** toolbar action.
3. On mouse/trackpad press, the frontend starts a new stroke and records the first point in the canvas's logical coordinate system.
4. While the input is held, mouse-move events append coordinate pairs to that stroke and update the Konva line for immediate visual feedback. These moves update frontend drawing state; they do not each trigger a database write or image export.
5. On release, the frontend completes the stroke. The student can draw additional strokes in the same drawing session.
6. When the student chooses **Finish** or **Save**, the frontend sends the completed vector drawing data to the backend. The backend validates the student's identity and access to the parent object, then stores the drawing record.
7. When the drawing is opened later, the frontend recreates Konva lines from the stored stroke data.

This proposal saves one vector drawing payload when the student finishes, rather than periodically saving rendered images. If the client wants protection against losing work before Finish/Save, consider saving completed strokes as vector data after each mouse release; that would still avoid 15-second image snapshots. Confirm which save boundary is expected.

## Coordinate capture and proposed data

Konva's React free-drawing example follows this model: start a line on mouse-down, use the stage pointer position, append points during mouse-move, and stop on mouse-up. A Konva `Line` stores its points as a flat sequence of x/y coordinates, for example `[x1, y1, x2, y2, ...]`. See [Konva's React free-drawing guide](https://konvajs.org/docs/react/Free_Drawing.html) and [Konva.Line points](https://konvajs.org/api/Konva.Line.html).

Candidate document shape, for discussion only:

```json
{
  "schemaVersion": 1,
  "canvas": { "width": 1000, "height": 700 },
  "strokes": [
    {
      "points": [24, 38, 26, 40, 30, 44],
      "color": "#1f2937",
      "width": 3
    }
  ]
}
```

- Store canvas-local coordinates rather than page or screen coordinates. Include the logical canvas dimensions so the frontend can scale the drawing if the display size changes.
- Each stroke can contain its coordinate pairs and the visual properties needed to redraw it, such as color and width. Add ordering and timestamps only if product requirements need them.
- The authenticated student identity should come from the server's JWT context, not from a trusted client-supplied student ID.
- The exact PostgreSQL schema and API request/response contract remain to be designed. A structured vector representation is the proposed source of truth; a rendered image may be generated later for export or preview if needed, but is not the save mechanism proposed here.
- For long sessions, assess payload size and point reduction after real usage is understood. Do not discard points in a way that noticeably changes the student's stroke.

Konva's React guidance recommends managing and serializing application state rather than relying on full-stage JSON for a larger React application. The stored app data should therefore be the drawing model (canvas metadata and strokes), not Konva node internals. See [Konva serialization best practices](https://konvajs.org/docs/data_and_serialization/Best_Practices.html) and [React stage serialization guidance](https://konvajs.org/docs/data_and_serialization/Serialize_a_Stage.html).

## Initial functional requirements to validate

| ID | Proposed requirement | Acceptance evidence to define |
|---|---|---|
| FD-01 | A student can enter and exit free-draw mode. | [TODO: Verify tool state and keyboard-operable controls.] |
| FD-02 | On a laptop, the student can draw a freehand stroke with a mouse or trackpad. | Verify press, move, release, and that a release outside the canvas does not leave drawing stuck. |
| FD-03 | The frontend captures the stroke's canvas-local coordinate pairs from input start through input release and renders the stroke while drawing. | Compare captured model data with the rendered stroke during implementation. |
| FD-04 | The drawing is saved as vector coordinates when the student selects Finish/Save; no periodic image snapshots are required. | Inspect the saved record and confirm it can be reconstructed as Konva lines. |
| FD-05 | The toolbar action has an understandable icon and accessible name. | [TODO: Design and accessibility review.] |
| FD-06 | Saved drawings are only accessible to authorized students and relevant project members. | [TODO: Define parent object and permission checks.] |

These are proposed acceptance criteria, not implementation results. iPad and Apple Pencil support is explicitly deferred.

## Konva and icon responsibilities

- **Konva / react-konva:** Candidate canvas scene graph and freehand rendering approach for the React frontend. The React guide demonstrates storing strokes as vector data and rendering them as Konva lines. Confirm the package and version before implementation.
- **Icon:** A separate toolbar asset that communicates the free-draw action. A pencil/pen symbol is proposed. Keep an accessible name such as “Free draw.”
- **Radix UI:** Could provide accessible UI primitives around tool controls; it does not itself settle the icon choice.
- **Tailwind CSS:** Could style the toolbar and surrounding layout within the planned frontend stack.
- **TypeScript:** Could describe stroke state and the drawing payload after the API boundary is agreed.

No implementation, performance testing, or browser compatibility testing has been performed.

## Candidate API and persistence questions

A future Django REST Framework endpoint could accept one completed drawing payload when the student chooses Finish/Save. Before implementation, decide:

- Which group, task, or other object owns each drawing.
- Whether to submit the full drawing session once on Finish/Save, or persist each completed stroke to reduce work lost if the page closes unexpectedly.
- Which fields and limits belong in the stored record.
- Whether drawings can be edited, exported, or deleted, and the retention policy.
- How the server checks JWT identity and membership permissions.

Do not write the database schema or endpoint contract until those requirements are confirmed.

## Real-time collaboration and AI

Django Channels and Daphne are part of the planned stack, but their inclusion does not mean this drawing feature is collaborative. Live stroke synchronization is outside the current proposal unless the client asks for shared real-time drawing. No drawing-to-Azure-OpenAI behavior is defined; do not send drawings to an AI service without explicit product and privacy approval.

## Security, privacy, and accessibility questions

- Apply the same access policy as the parent group/task/workspace.
- Derive student identity from the authenticated server context and validate access on every save/load operation.
- Confirm whether drawings may contain personal or sensitive information and define retention/deletion behavior.
- Provide an accessible name, focus behavior, keyboard-operable controls, and a non-canvas way to understand or operate key actions where feasible.
- First-release input scope is laptop mouse/trackpad. Revisit touch and Apple Pencil behavior in a later phase.

## Open decisions

- Exact student workflow and parent object.
- Whether a session is saved on Finish/Save or completed strokes are saved one-by-one.
- Icon library and approved symbol.
- Required drawing controls for the initial release.
- Edit, export, deletion, and retention policy.
- Individual versus shared drawing; real-time drawing is not assumed.
- Whether drawings connect to any AI functionality.
- Browser support and performance expectations for long strokes.

## Next steps

1. Confirm the student workflow and parent object with the client.
2. Confirm the save boundary: finish the complete drawing session, or save vector strokes after each release.
3. Obtain any existing repository, product brief, designs, and implementation handoff.
4. Confirm technology versions and whether Konva/react-konva fits the expected UX.
5. Define authorization, schema, and retention before implementation planning.
6. Defer iPad and Apple Pencil interaction requirements to a later phase.

## Technical references

- [Konva: free drawing with React](https://konvajs.org/docs/react/Free_Drawing.html)
- [Konva.Line points API](https://konvajs.org/api/Konva.Line.html)
- [Konva: serialization best practices](https://konvajs.org/docs/data_and_serialization/Best_Practices.html)
- [Konva: React stage serialization](https://konvajs.org/docs/data_and_serialization/Serialize_a_Stage.html)
