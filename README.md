# ShiftBridge

**ShiftBridge** is a chat-first workplace operations platform designed for small and medium-sized businesses. It brings team communication, task tracking, shift visibility, and handovers into one workspace, so important employee reports are less likely to get buried in group messages or disconnected spreadsheets.

Project status: Frontend prototype available. Backend, real-time collaboration, and autonomous AI workflows are in development or planned.

Challenge: Track 2 — Tencent WorkBuddy  
Presentation: https://drive.google.com/file/d/1LlCP8xnzoaEbRFuKsKvXN8t2y2UaBbrx/view?usp=drive_link

1. The Problem

In small businesses such as cafés, small business companies, shops, and service teams, staff often report problems or communicate updates
through group chats and manual records. When messages pile up, supervisors may overlook urgent issues, responsibilities may be unclear, 
and unfinished work can be lost between shifts.

ShiftBridge addresses three operational gaps:

- Visibility: Important reports are difficult to distinguish from everyday chat.
- Accountability: Employees may not know who owns a task or whether it has been addressed.
- Continuity: Open issues and updates are not always transferred clearly to the next shift.

 2. Our Solution

ShiftBridge uses a familiar messaging interface as the team's starting point, with connected views for tasks, shifts, and handovers. 
Rather than expecting employees to switch between multiple tools, the platform is designed to turn relevant workplace conversations into traceable actions.

Core design principle: Keep team chat familiar; make work visible and trackable.

Frontend prototype — available now

| Area | What the current prototype demonstrates |
| --- | --- |
| Team Chat | A chat-first interface with demonstration messages and familiar navigation. |
| Tasks | Task lists, filters, statuses, and prototype task actions. |
| Shifts | Shift-related views and demonstration clock-in/clock-out interactions. |
| Handovers | A structured handover form for passing information between shifts. |
| Manager / Admin | Management screens, unresolved-issue visibility, and a Needs Attention area. |
| Workspaces | A workspace switcher for the interface. |
| AI Settings | A demonstration interface for future AI functionality; no live autonomous agent is connected yet. |

The current interface is responsive on mobile and desktop. Prototype data and interactions may use local browser storage and 
are not evidence of real multi-user synchronization.

 3. Intended AI-Assisted Workflow

Target workflow
1. Employee posts an update or reports an issue.
2. The AI interprets the message and identifies actionable requests.
3. The system checks permissions, duplicates, employee eligibility, shift availability, and workload.
4. An authorized task is created or suggested.
5. Routine actions may proceed automatically, while sensitive or unclear actions require human approval.
6. Task progress and unresolved follow-ups are tracked.
7. Open issues are included in the next shift's handover.

A task being marked completed does not automatically mean the original issue has been resolved. 
The intended system should keep verification and follow-up visible where needed.

 How We Used Tencent WorkBuddy

Tencent WorkBuddy was used as a project-development assistant, helping the team move through three stages: **Define → Build → Communicate**.

| Stage | WorkBuddy's role |
| --- | --- |
| Define | Support problem framing, solution planning, and workflow ideas. |
| Build | Assist development work, UI refinements, and technical exploration. |
| Communicate | Help structure project explanations and presentation material. |

WorkBuddy's use during development is separate from an AI agent running inside ShiftBridge. 

## 5. Planned Agent Responsibilities

The proposed AI workflow separates responsibilities to make decisions more understandable and controllable.

1. Message Understanding Agent: Identify actionable employee reports, requests, and updates.
2. Policy and Assignment Agent:Check permissions, task duplicates, employee eligibility, shift availability, and workload before suggesting or assigning work.
3. Progress and Follow-up Agent: Monitor task updates and flag unresolved or overdue work.
4. Handover Agent: Prepare a concise summary of open issues and the next shift's priorities.

## The evidences are provided separately in the different folder.
6. Technology Stack

### Used in the Current Frontend

- HTML5: Interface structure.
- CSS3: Responsive styling.
- Vanilla JavaScript (ES modules): Interface behavior.
- Browser localStorage: Local prototype state.
- Hash-based routing:Frontend navigation.
- GitHub: Source control and project submission.

These planned services are not claimed to be operational until the repository and demo demonstrate them.

 Team and Acknowledgements

**Team:** [Team Hj, Phoo Myat Nay Chi, Soe Min Khant]

Developed for a Tencent WorkBuddy hackathon challenge (Track 2).

Tencent WorkBuddy supported the team's project-development workflow; any future product integration will be documented separately.

---

*ShiftBridge — One team chat. Smarter workdays.*

