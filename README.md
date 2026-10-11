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


ShiftBridge — Silent AI agent for team shift handover
ShiftBridge is a shared backend for small-business team communication with operational task management and a Silent AI reasoning agent that monitors workspace activity. Built for DORMATHON 2026 with WorkBuddy Agentic Solutions.

The single group chat is the home screen for employees and administrators. On mobile a large raised Chat button sits between Tasks and Shift buttons; administrators also have a Manage area with Silent AI Proposals.

Architecture
Frontend: Vanilla HTML/CSS/JavaScript (no React/Next.js)
Backend: Node.js + Express 5 + SQLite (better-sqlite3)
MCP Server: Official @modelcontextprotocol/sdk (v1.32.1), stdio transport, 8 AI tools
Real-time sync: Server-Sent Events (SSE) + 2-second polling fallback
Database: Single SQLite file at server/shiftbridge.db
The backend is the single source of truth for all shared data: messages, tasks, issues, workspaces, rules, shifts, handovers, and AI proposals. Each phone persists only its selected demo identity in localStorage.

Quick start
# Install dependencies (includes MCP SDK)
npm install

# Start the backend (serves both API and static frontend)
npm run dev
The server starts on 0.0.0.0:3000. The console will print:

Local: http://localhost:3000
Network: http://<your-laptop-ipv4>:3000 (for phone access)
Open http://localhost:3000 on your laptop, and http://<laptop-ip>:3000 on phones connected to the same Wi-Fi.

Silent AI Agent (MCP Integration)
The Silent AI agent connects via Model Context Protocol (MCP) with stdio transport, using the official @modelcontextprotocol/sdk. It monitors workspace activity and creates proposals that managers review in the dashboard.

Connecting WorkBuddy Desktop
The MCP config is at ~/.workbuddy-ai/mcp.json:

{
  "mcpServers": {
    "shiftbridge": {
      "command": "C:\\Users\\<user>\\.workbuddy-ai\\binaries\\node\\versions\\22.22.2-6\\node.exe",
      "args": ["C:\\<project-path>\\server\\mcp-server.js"]
    }
  }
}
After adding the config, open WorkBuddy Desktop → Connectors → trust the new MCP server.

MCP Tools (8)
Tool	Description
get_recent_messages	Read recent chat messages from a workspace (IDs, sender, body, timestamp)
get_active_tasks	List all tasks with status, assignee, category, verification, and protected flags
get_workspace_rules	Show permitted (self-report) and locked (qualified) categories per workspace
list_tasks	List all tasks in a workspace (alias of get_active_tasks)
propose_task	Propose a new task with evidence and AI reasoning for manager review
propose_completion	Review a completion claim, gather evidence, produce AI reasoning, create proposal
refuse_protected_work	Create a refusal proposal for protected work lacking qualified verification
get_audit_trail	Retrieve the full audit log for a workspace
Protected Task Enforcement
Tasks in repairs, purchases, or safety categories automatically get verification: 'qualified'. When an employee tries to mark these as done, the server redirects the status to review instead — the completion claim is preserved but requires qualified review before final approval.

CRITICAL SAFETY: Qualified Verification Requirement
When a manager approves a completion_review proposal for a protected task (repairs, purchases, safety, or any task with verification: 'qualified'):

Without qualified verification evidence → the task remains in review status. The approval is recorded, but a demo manager role alone is NOT qualified verification.
With explicit qualified verification evidence (e.g., technician report, inspection certificate) → the task is marked done.
The manager dashboard prompts for qualified verification evidence when approving a protected completion review. The audit log records whether verification evidence was provided.

API endpoints
Method	Path	Description
GET	/api/workspaces	List all workspaces with members & rules
POST	/api/workspaces	Create a new workspace
PUT	/api/workspaces/:id	Update workspace settings
GET	/api/workspaces/:ws/messages	List messages (supports ?since=timestamp)
POST	/api/workspaces/:ws/messages	Send a message (idempotent by client ID)
GET	/api/workspaces/:ws/tasks	List all tasks
POST	/api/workspaces/:ws/tasks	Create a task (auto-sets qualified verification for protected categories)
GET	/api/tasks/:id	Get a single task
PUT	/api/tasks/:id	Update task (server enforces review for protected tasks)
GET	/api/workspaces/:ws/issues	List issues
GET	/api/issues/:id	Get a single issue
PUT	/api/issues/:id	Update issue (resolve, approve, etc.)
PUT	/api/rules/:id	Toggle a rule (locked rules cannot be changed)
GET	/api/workspaces/:ws/proposals	List AI proposals (supports ?status=pending)
GET	/api/proposals/:id	Get a single proposal
POST	/api/workspaces/:ws/proposals	Create an AI proposal (task_proposal, completion_review, refusal)
PUT	/api/proposals/:id/review	Approve or reject a proposal (with qualifiedVerification for protected tasks)
GET	/api/workspaces/:ws/shift	Get shift state
PUT	/api/workspaces/:ws/shift	Clock in/out
GET	/api/workspaces/:ws/handover	Get handover
PUT	/api/workspaces/:ws/handover	Save handover
GET	/api/workspaces/:ws/audit	Administrator review records (audit log)
GET	/api/sync?workspace=X&revision=N	Polling sync check
GET	/api/events?workspace=X	SSE real-time event stream
GET	/api/people	List demo people
GET	/api/health	Health check
POST	/api/reset	Reset database to seed data
Screens and URLs
#/chat — one shared group conversation per workspace
#/tasks and #/task/:id — My Tasks, task detail, status changes
#/shift, #/handover — attendance and shift handover
#/profile — demo identity, profile and workspace switcher
#/manage — admin overview with Silent AI Proposals section
#/manage/attention — unresolved issues and review items
#/manage/proposals — all AI proposals (pending and reviewed)
#/manage/all-work — all workspace tasks and issues
#/manage/team — members and shift coverage
#/manage/invites — sample invite code
#/manage/rules — AI auto-assignment permissions
#/manage/settings — workspace details
#/manage/issue/:id — evidence, inspection approval and resolution
Development
npm run check          # Syntax-check all JS files
npm run test:backend   # Run backend integration tests (19 tests)
npm run seed           # Re-seed the database
npm run mcp            # Start MCP server (for manual testing)
Project structure
├── index.html              # App mount point
├── styles.css             # All styling (mobile-first, responsive)
├── src/
│   ├── app.js             # Main app: routing, rendering, API integration, proposals
│   ├── api.js             # API client (fetch wrapper, proposals methods)
│   ├── data.js            # Demo people, helpers, identity storage
│   └── icons.js           # Inline SVG icons
├── server/
│   ├── index.js           # Express server (static + API + SSE + proposals + enforcement)
│   ├── db.js              # SQLite schema and row mappers (includes ai_proposals table)
│   ├── seed.js            # Initial demo data seeding
│   ├── rule-defaults.js   # Shared rule definitions (locked: repairs, purchases, safety)
│   ├── mcp-server.js      # MCP server (official SDK, stdio transport, 8 tools)
│   ├── test.js            # 19 backend integration tests
│   └── shiftbridge.db     # SQLite database (auto-created, gitignored)
└── assets/
    └── mark.svg            # ShiftBridge logo
Known limitations
No authentication — demo identities are simulated and not secure
No file uploads — photo attachment button shows a notice
LAN-only — do not expose this backend to the public internet
Safety-sensitive work — equipment repairs, spending, and safety certification are never silently authorized; server-side enforcement redirects done → review for protected tasks, and manager approval of completion reviews requires explicit qualified verification evidence to mark tasks done
MCP connector trust — the ShiftBridge MCP connector must be manually trusted in WorkBuddy Desktop before it can be invoked from chat

