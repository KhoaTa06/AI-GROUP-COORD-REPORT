# Sprint 1 Report — Planning and Feature Definition

- Sprint dates: October 11
- Team members: Khoa Ta, Jayden Blewett, Iyke Odum
- Status: Planning only; no implementation was supplied or performed.

## Sprint goal

Set a shared direction for the AI Group Coordinator project, record the proposed technology stack, and scope a free-drawing feature for future implementation. The client did not provide code for continuation of an existing project, so this sprint documents plans and decisions to confirm rather than reporting completed software.

## Planned work

| Item | Planned outcome | Status |
|---|---|---|
| Establish project and repository scope | Reports-only repository; implementation is out of scope here | Documented |
| Record target technology stack | Baseline recorded from the project brief; versions and details still need confirmation | Documented |
| Define free-drawing use case | Initial feature proposal, interaction flow, and acceptance questions | Drafted |
| Discuss drawing canvas and toolbar icon | Record Konva/react-konva role and separate icon choice from canvas rendering | Drafted |
| Plan validation and follow-up | Identify UX, persistence, collaboration, accessibility, and client questions | Open |

## Proposed technology baseline

The following stack was supplied for the project and is recorded here as the planned target. This report does not claim that dependencies have been installed or integrated.

| Area | Planned technology |
|---|---|
| Frontend | React 19, TypeScript, Vite, Tailwind CSS, Radix UI |
| Drawing canvas | Konva through the React binding `react-konva` (confirm package and version) |
| Backend API | Python 3.12, Django, Django REST Framework |
| Database | PostgreSQL hosted on Azure |
| Authentication | JWT with SimpleJWT |
| Real-time communication | Django Channels and Daphne for WebSockets |
| AI integration | Microsoft Semantic Kernel and OpenAI SDK connected to Azure OpenAI |

The icon package was not specified. The planning notes list options for a free-draw toolbar icon; the team should choose one that fits the approved design system.

## Planning outcomes

- Captured an initial free-drawing feature proposal in [Free Drawing Feature Plan](Free_Drawing_Feature_Plan.md).
- Recorded the target stack and tool roles in [Planning Discussion Notes](../MoM/Sprint1_Planning_Discussion.md).
- Identified open questions around saving drawings, collaboration, access control, and the final icon.
- No code, running application, test results, or demo recording is claimed for this sprint.

## Challenges and changes

The main constraint is the absence of a codebase or implementation handoff for continuing an existing product. The work is therefore framed as requirements and design planning. Product details that were not supplied remain marked as questions or proposals.
