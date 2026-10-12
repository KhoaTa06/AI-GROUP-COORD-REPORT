# Sprint 1 Planning Discussion Notes

> Draft notes synthesized from the project brief and client clarifications. These are not verbatim meeting minutes. Confirm the date, attendees, exact discussion, and client decisions with the team before treating them as formal minutes.

- Date and time: [TODO]
- Attendees: [TODO]
- Note taker: [TODO]
- Status: Draft planning record

## Context and scope

The client provided no codebase for continuing an existing project. Sprint 1 is therefore scoped to planning, feature definition, and documenting the proposed stack. No implementation or technical integration is claimed. This repository stores reports only.

## Technology and tool discussion

The listed stack is the project target supplied by the user. The notes below assign intended roles; they do not assert that the tools are installed or that choices beyond the supplied stack have been approved.

| Tool / technology | Planned role | Planning note |
|---|---|---|
| React 19 | Frontend UI | React application for coordinator workflows and drawing controls. |
| TypeScript | Frontend types | Model drawing tools, stroke data, and API payloads with explicit types. |
| Vite | Frontend development/build tool | Proposed frontend project tooling. |
| Tailwind CSS | Styling | Style the page and toolbar using utility classes. |
| Radix UI | Accessible UI primitives | Use for suitable controls and dialogs; confirm component choices. |
| Konva / react-konva | Canvas drawing | Candidate canvas and stroke-rendering layer. The free-draw plan captures line coordinates in frontend state and persists vector data at the agreed save boundary. |
| Python 3.12 | Backend runtime | Target Python version from the project brief. |
| Django | Backend framework | Application framework and server-side domain logic. |
| Django REST Framework | HTTP API | Potential API for saving and retrieving completed drawing data, subject to final design. |
| PostgreSQL on Azure | Database | Target relational database and hosting platform. Choose the Azure PostgreSQL offering and operational details later. |
| SimpleJWT | JWT authentication | JWT issuance/refresh for API authentication; confirm token lifetime and authorization policy. |
| Django Channels | Real-time backend | Potential WebSocket support if live multi-user drawing is required. |
| Daphne | ASGI server | Proposed ASGI server for Django Channels / WebSocket support. |
| Microsoft Semantic Kernel | AI orchestration | AI integration layer as supplied; its role in drawing workflows remains to be defined. |
| OpenAI SDK | Model API client | Connect to Azure OpenAI as planned; confirm supported SDK configuration with the implementation team. |
| Azure OpenAI | AI service | Planned model endpoint; model deployment, region, quotas, and privacy settings remain to be confirmed. |

### Free-draw canvas, coordinate saving, and icon discussion

- The canvas and the toolbar icon are separate concerns. Konva/react-konva would handle the drawing surface and stroke interactions; an icon library or approved custom SVG would render the toolbar symbol.
- Proposed control: a clearly labeled free-draw action with a pencil/pen-style icon. A text label or accessible name should remain available so meaning does not depend on the icon alone.
- Icon source remains undecided. Candidate approaches are an icon set already approved by the team, Radix Icons if the team chooses to add that package, or a project-owned SVG. The stack list names Radix UI primitives but does not confirm that Radix Icons or another icon package is installed.
- **Client clarification:** For saving students' drawings, do not save an image every 15 seconds. Freeman suggested tracking the drawing coordinates from when a student starts drawing until they finish.
- **Proposed technical approach:** On mouse/trackpad press, start a stroke and record its first canvas-local point. Append coordinate pairs while the input is held and update the Konva line for on-screen feedback. On release, finish the stroke. On Finish/Save, send the drawing's vector stroke data to the backend once. Do not write to the database or export an image on every mouse-move event.
- A drawing session may contain multiple strokes. Open choice: save the complete session once on Finish/Save, or persist completed vector strokes after each release to reduce work lost if a student closes the page early. Neither policy is approved yet.
- Candidate saved data includes canvas dimensions and ordered stroke records with point pairs and visual properties such as color and width. Use logical canvas coordinates rather than browser page coordinates; confirm how to handle resizing before setting the persisted format.
- Konva's official React free-drawing example tracks a line's points and renders them as vector lines. Konva's serialization guidance recommends serializing application state in React rather than relying on the full stage tree. References: [React free drawing](https://konvajs.org/docs/react/Free_Drawing.html), [Line points](https://konvajs.org/api/Konva.Line.html), [serialization best practices](https://konvajs.org/docs/data_and_serialization/Best_Practices.html).
- **Input scope for the first release:** laptop trackpad or mouse. iPad and Apple Pencil support is deferred. Do not include touch or stylus support in first-release acceptance criteria.
- Confirm whether a drawing is attached to a group, task, meeting, or another project object before specifying authorization and save/load behavior.
- Live shared drawing would require an agreed collaboration model and likely Channels/WebSockets. The presence of Channels in the proposed stack does not establish that collaborative drawing is in scope.

## Proposed decisions to confirm

| Topic | Current planning position | Confirmation needed |
|---|---|---|
| Feature scope | Basic free-draw canvas for a student workflow | Client use case, intended parent object, and priority |
| Canvas technology | Evaluate Konva via react-konva for the React frontend | Package/version and fit for expected interactions |
| Input devices | Laptop mouse/trackpad for initial scope | Confirm browser support; defer iPad/Apple Pencil |
| Drawing persistence | Capture coordinates and save vector data, not periodic image snapshots | Save full session on Finish/Save or completed strokes on release; schema and retention |
| Toolbar symbol | Pencil/pen-style free-draw icon with an accessible label | Approved icon source and exact symbol |
| Collaboration | Not decided; real-time drawing is not assumed | Whether multiple users must see each other's strokes live |
| AI relationship | No drawing-to-AI behavior defined | Whether sketches are ever submitted to an AI workflow |
| Technology baseline | Record stack supplied in the project brief | Team/client approval, versions, hosting details, and integration boundaries |

## Questions for the client and team

1. What student task should free drawing support, and which group/task/workspace should own the drawing?
2. Should the completed drawing be saved only when the student selects Finish/Save, or should each completed stroke also be saved for recovery?
3. Which controls are required for the first release (colors, stroke widths, eraser, undo/redo, clear)?
4. Who can view, edit, export, or delete drawings, and how long are they retained?
5. Is this a personal sketch or a shared whiteboard? Does simultaneous drawing require WebSocket synchronization?
6. What icon library or design source is approved, and should the toolbar show a text label?
7. What client repository, requirements, design files, and handoff materials are available for future implementation?
8. Which Azure PostgreSQL and Azure OpenAI deployment details are approved for the project?

## Action items

| Action | Owner | Due date | Status |
|---|---|---|---|
| Confirm dates, attendees, and whether these notes reflect an actual meeting | [TODO] | [TODO] | Open |
| Validate the student workflow, parent object, and required controls with the client | [TODO] | [TODO] | Open |
| Confirm whether to save a session on Finish/Save or each completed stroke | [TODO] | [TODO] | Open |
| Select icon source and symbol with the design team | [TODO] | [TODO] | Open |
| Confirm permissions, schema, and retention requirements | [TODO] | [TODO] | Open |
| Confirm stack versions and Azure deployment assumptions | [TODO] | [TODO] | Open |
| Obtain code or repository handoff if continuation of an existing product is expected | [TODO] | [TODO] | Open |
