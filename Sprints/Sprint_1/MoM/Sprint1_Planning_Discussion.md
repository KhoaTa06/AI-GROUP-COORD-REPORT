# Sprint 1 Planning Discussion Notes

> Draft notes synthesized from the project brief for planning. These are not verbatim meeting minutes. Confirm the date, attendees, exact discussion, and client decisions with the team before treating them as formal minutes.

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
| Konva / react-konva | Canvas drawing | Konva provides canvas-based shapes and interaction; react-konva exposes a React-oriented scene graph. Confirm the exact dependency and version before implementation. |
| Python 3.12 | Backend runtime | Target Python version from the project brief. |
| Django | Backend framework | Application framework and server-side domain logic. |
| Django REST Framework | HTTP API | API endpoints for drawing metadata and other application data, subject to the final design. |
| PostgreSQL on Azure | Database | Target relational database and hosting platform. Choose the Azure PostgreSQL offering and operational details later. |
| SimpleJWT | JWT authentication | JWT issuance/refresh for API authentication; confirm token lifetime and authorization policy. |
| Django Channels | Real-time backend | Potential WebSocket support if live multi-user drawing is required. |
| Daphne | ASGI server | Proposed ASGI server for Django Channels / WebSocket support. |
| Microsoft Semantic Kernel | AI orchestration | AI integration layer as supplied; its role in drawing workflows remains to be defined. |
| OpenAI SDK | Model API client | Connect to Azure OpenAI as planned; confirm supported SDK configuration with the implementation team. |
| Azure OpenAI | AI service | Planned model endpoint; model deployment, region, quotas, and privacy settings remain to be confirmed. |

### Free-draw canvas and icon discussion

- The canvas and the toolbar icon are separate concerns. Konva/react-konva would handle the drawing surface and stroke interactions; an icon library or approved custom SVG would render the toolbar symbol.
- Proposed control: a clearly labeled free-draw action with a pencil/pen-style icon. A text label or accessible name should remain available so meaning does not depend on the icon alone.
- Icon source remains undecided. Candidate approaches are an icon set already approved by the team, Radix Icons if the team chooses to add that package, or a project-owned SVG. The stack list names Radix UI primitives but does not confirm that Radix Icons or another icon package is installed.
- Candidate interaction: select the free-draw tool, draw with pointer or touch, finish a stroke on pointer release, and allow the user to exit drawing mode. Color, width, erasing, undo/redo, and clearing should be confirmed for the first release.
- Confirm whether a drawing is attached to a group, task, meeting, or another project object before specifying save/load behavior.
- If a freehand stroke is represented by a Konva line, implementation should verify smooth pointer tracking, coordinate handling under resize/zoom, and performance for long strokes. These are design considerations, not tested results.
- Live shared drawing would require an agreed collaboration model and likely Channels/WebSockets. The presence of Channels in the proposed stack does not establish that collaborative drawing is in scope.

## Proposed decisions to confirm

| Topic | Current planning position | Confirmation needed |
|---|---|---|
| Feature scope | Define a basic free-draw canvas for a coordinator workflow | Client use case, intended users, and priority |
| Canvas technology | Evaluate Konva via react-konva for the React frontend | Package/version and fit for the expected interactions |
| Toolbar symbol | Pencil/pen-style free-draw icon with an accessible label | Approved icon source and exact symbol |
| Drawing persistence | Not decided | What object owns a drawing, format, retention, and permissions |
| Collaboration | Not decided; real-time drawing is not assumed | Whether multiple users must see each other's strokes live |
| AI relationship | No drawing-to-AI behavior defined | Whether sketches are ever submitted to an AI workflow |
| Technology baseline | Record stack supplied in the project brief | Team/client approval, versions, hosting details, and integration boundaries |

## Questions for the client and team

1. What user task should free drawing support, and who will use it?
2. Is the feature a personal sketch pad, a drawing attached to a group artifact, or a shared whiteboard?
3. Which devices and input types must be supported (mouse, touch, stylus)?
4. Which controls are required for the first release (colors, stroke widths, eraser, undo/redo, clear)?
5. Should drawings save automatically, on explicit save, or not persist?
6. If saved, who can view, edit, export, or delete them, and how long are they retained?
7. Does simultaneous drawing require WebSocket synchronization, or is real-time communication for another feature?
8. What icon library or design source is approved, and should the toolbar show a text label?
9. What client repository, requirements, design files, and handoff materials are available for future implementation?
10. Which Azure PostgreSQL and Azure OpenAI deployment details are approved for the project?

## Action items

| Action | Owner | Due date | Status |
|---|---|---|---|
| Confirm dates, attendees, and whether these notes reflect an actual meeting | [TODO] | [TODO] | Open |
| Validate the free-draw use case and required controls with the client | [TODO] | [TODO] | Open |
| Select icon source and symbol with the design team | [TODO] | [TODO] | Open |
| Decide persistence and sharing requirements | [TODO] | [TODO] | Open |
| Confirm stack versions and Azure deployment assumptions | [TODO] | [TODO] | Open |
| Obtain code or repository handoff if continuation of an existing product is expected | [TODO] | [TODO] | Open |
