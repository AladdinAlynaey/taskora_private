> [!CAUTION]
> **NOTICE: The main codebase is a private repository.**
> This repository contains the public structure and architecture overview. If you would like to collaborate, contribute, or request access to the actual source code, please contact me directly.
> - **Website:** https://alaadin-alynaey.site/
> - **Live App:** https://taskora.alaadin-alynaey.site/



> [!CAUTION]
> **STRICT VIEW-ONLY REPOSITORY: NO USE, NO RUNNING, NO DEPLOYMENT ALLOWED.**
> This repository is made public **STRICTLY FOR VIEWING PURPOSES ONLY** (e.g., as a portfolio demonstration). 
> You are **ABSOLUTELY PROHIBITED** from downloading, running, testing, executing, modifying, copying, or distributing this application, its source code, or any of its assets under any circumstances, for any purpose (personal, commercial, or educational). Please see the [LICENSE](LICENSE) file for the full, legally binding restrictive terms.

<div align="center">

# ⚡ TASKORA

### _The Enterprise Project Management System That Actually Gets Things Done_

<br>

[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-3.x-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![Elasticsearch](https://img.shields.io/badge/Elasticsearch-8.x-005571?style=for-the-badge&logo=elasticsearch&logoColor=white)](https://www.elastic.co/)
[![Gunicorn](https://img.shields.io/badge/Gunicorn-gevent-499848?style=for-the-badge&logo=gunicorn&logoColor=white)](https://gunicorn.org/)
[![AI Powered](https://img.shields.io/badge/AI-Gemini%20Powered-8E75B2?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev/)
[![PM2](https://img.shields.io/badge/PM2-Production-2B037A?style=for-the-badge&logo=pm2&logoColor=white)](https://pm2.keymetrics.io/)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)](LICENSE)

<br>

**Multi-Workspace** · **Elasticsearch Powered** · **AI Assistant** · **Kanban & Scrum Boards**  
**Role-Based Access** · **Group Chat** · **Super Admin Panel** · **PM/TL Transfers** · **Dark Mode**

<br>

```
🏢 Workspaces  →  📁 Projects  →  👥 Teams  →  📝 Issues  →  ✅ Done
```

<br>

> _"One platform. Every project. Every team. Zero chaos."_

---

</div>

<br>

## 📑 Table of Contents

<details>
<summary><b>Click to expand</b></summary>

- [✨ Why Taskora?](#-why-taskora)
- [🖥️ Screenshots](#️-screenshots)
- [🏗️ Architecture](#️-architecture)
- [🚀 Quick Start](#-quick-start)
- [⚙️ Production Deployment](#️-production-deployment)
- [🎯 Core Concepts](#-core-concepts)
- [👥 Role System](#-role-system)
- [📊 Permissions Matrix](#-permissions-matrix)
- [🏢 Workspaces](#-workspaces)
- [📁 Projects & Boards](#-projects--boards)
- [👥 Teams](#-teams)
- [📝 Issues & Workflow](#-issues--workflow)
- [🤖 AI Assistant](#-ai-assistant)
- [💬 Messaging & Notifications](#-messaging--notifications)
- [🔄 PM/TL Transfer System](#-pmtl-transfer-system)
- [⚡ Super Admin Panel](#-super-admin-panel)
- [📈 Statistics & Reporting](#-statistics--reporting)
- [🌗 Dark Mode](#-dark-mode)
- [📚 Documentation Portal](#-documentation-portal)
- [🌐 Environment Variables](#-environment-variables)
- [📂 Project Structure](#-project-structure)
- [❓ FAQ](#-faq)
- [🔧 Troubleshooting](#-troubleshooting)
- [📜 Changelog](#-changelog)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

</details>

---

## ✨ Why Taskora?

Most project management tools are either **too simple** for real teams or **too bloated** to actually use. Taskora hits the sweet spot:

<table>
<tr>
<td width="50%">

### 🎯 What Makes It Different

- **🏢 True Multi-Workspace** — Complete data isolation between organizations
- **🤖 AI-Powered Assistant** — Ask questions about your projects in natural language
- **🔐 6 Granular Roles** — From Owner to Viewer, everyone has the right permissions
- **📋 Approval Workflows** — Issues go through proper review before work begins
- **💬 Built-in Messaging** — Direct messages, workspace chat, and group conversations
- **📊 Deep Analytics** — Per-user, per-team, and per-project statistics
- **🌗 Premium Dark Mode** — Beautiful, eye-friendly dark theme
- **📱 Mobile-First UI** — Bottom navigation, responsive design, native-app feel
- **🌍 Bilingual Docs** — Full documentation in English and Arabic

</td>
<td width="50%">

### 📊 By The Numbers

| Metric | Value |
|--------|-------|
| **Python Modules** | 31 backend modules |
| **HTML Templates** | 61 responsive pages |
| **Core App** | ~5,700 lines of Flask routes |
| **Database** | Elasticsearch 8.x |
| **AI Integration** | 6 specialized modules |
| **Concurrent Users** | ~3,000 simultaneous |
| **Worker Type** | Gevent async (non-blocking) |
| **Uptime** | Auto-restart via PM2 + systemd |

</td>
</tr>
</table>

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                              TASKORA ARCHITECTURE                            │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   Client (Browser)                                                           │
│   ┌──────────────────────────────────────────────────────────────┐           │
│   │     Mobile-First UI  │    Dark Mode   │      AI Widget       │           │
│   └──────────────────────────┬───────────────────────────────────┘           │
│                              │ HTTPS                                         │
│                              ▼                                               │
│   Reverse Proxy (Caddy/Nginx)                                                │
│                              │                                               │
│                              ▼                                               │
│   ┌──────────────────────────────────────────────────────────────┐           │
│   │  PM2 Process Manager (auto-restart, file watching, logging)  │           │
│   └──────────────────────────┬───────────────────────────────────┘           │
│                              │                                               │
│                              ▼                                               │
│   ┌──────────────────────────────────────────────────────────────┐           │
│   │  Gunicorn WSGI Server                                        │           │
│   │  ┌────────────┐  ┌────────────┐  ┌────────────┐              │           │
│   │  │ Worker 1   │  │ Worker 2   │  │ Worker 3   │  (gevent)    │           │
│   │  │ 1000 conn  │  │ 1000 conn  │  │ 1000 conn  │              │           │
│   │  └────────────┘  └────────────┘  └────────────┘              │           │
│   └──────────────────────────┬───────────────────────────────────┘           │
│                              │                                               │
│                              ▼                                               │
│   ┌──────────────────────────────────────────────────────────────┐           │
│   │  Flask Application (app.py - 5,700+ lines)                   │           │
│   │                                                              │           │
│   │  ┌─────────┐ ┌──────────┐ ┌──────────┐ ┌────────────────┐    │           │
│   │  │  Auth   │ │Workspaces│ │ Projects │ │  Issue Tracker │    │           │
│   │  │ System  │ │ Manager  │ │ Manager  │ │    + Approval  │    │           │
│   │  └─────────┘ └──────────┘ └──────────┘ └────────────────┘    │           │
│   │  ┌─────────┐ ┌──────────┐ ┌──────────┐ ┌─────────────────┐   │           │
│   │  │  Teams  │ │ Messages │ │Notifica- │ │   AI Assistant  │   │           │
│   │  │ Manager │ │ + Groups │ │  tions   │ │  (Gemini API)   │   │           │
│   │  └─────────┘ └──────────┘ └──────────┘ └─────────────────┘   │           │
│   └──────────────────────────┬───────────────────────────────────┘           │
│                              │                                               │
│                              ▼                                               │
│   ┌──────────────────────────────────────────────────────────────┐           │
│   │     Elasticsearch 8.x (localhost:9200)                       │           │
│   │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐     │           │
│   │  │  Users   │ │ Projects │ │  Issues  │ │   Messages   │     │           │
│   │  │  Index   │ │  Index   │ │  Index   │ │    Index     │     │           │
│   │  └──────────┘ └──────────┘ └──────────┘ └──────────────┘     │           │
│   │  + 13 more indices (teams, workspaces, notifications...)     │           │
│   └──────────────────────────────────────────────────────────────┘           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### Storage Engine

| Feature | Details |
|---------|--------|
| **Engine** | Elasticsearch 8.x |
| **Access** | Local only (`127.0.0.1:9200`) — not exposed to internet |
| **Indices** | 17 prefixed indices (`taskora_users`, `taskora_projects`, etc.) |
| **JVM Heap** | 512MB (configurable) |
| **Auto-Start** | systemd service (`elasticsearch.service`) |
| **Data Safety** | Managed by ES — automatic persistence, no file corruption |

---

## 🚀 Quick Start

### Prerequisites

- **Python 3.10+** — [Download](https://www.python.org/downloads/)
- **Elasticsearch 8.x** — [Download](https://www.elastic.co/downloads/elasticsearch)
- **Java 17+** — Required by Elasticsearch
- **Git** — [Download](https://git-scm.com/)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/AladdinAlynaey/taskora.git
cd taskora

# 2. Create & activate virtual environment
python -m venv venv
source venv/bin/activate          # Linux/Mac
# venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Start Elasticsearch
sudo systemctl start elasticsearch
curl http://localhost:9200          # Verify ES is running

# 5. Configure environment
cp .env.example .env
nano .env                          # Add your Gemini API keys

# 6. Run the application
python app.py
```

Then open **http://localhost:5000** in your browser 🎉

---

## ⚙️ Production Deployment

Taskora is production-ready with **Gunicorn + gevent + PM2** for maximum performance and reliability.

### Why This Stack?

| Component | Purpose | Why |
|-----------|---------|-----|
| **Elasticsearch** | Database | Fast, scalable search engine for persistent data |
| **Gunicorn** | WSGI Server | Industry-standard Python web server |
| **gevent** | Async Workers | Each worker handles 1,000+ concurrent connections |
| **PM2** | Process Manager | Auto-restart, file watching, log management, boot startup |

### Deploy with PM2

```bash
# 1. Install production dependencies
pip install gunicorn gevent

# 2. Start with PM2 (uses ecosystem.config.js)
pm2 start ecosystem.config.js

# 3. Save PM2 state (survives server reboot)
pm2 save

# 4. Enable auto-start on boot
pm2 startup systemd
# Run the command it gives you with sudo
```

### Configuration Files

| File | Purpose |
|------|---------|
| `ecosystem.config.js` | PM2 process config — name, script, env vars, file watching |
| `gunicorn.conf.py` | Gunicorn config — workers, timeouts, connections, logging |
| `/etc/elasticsearch/elasticsearch.yml` | ES config — cluster name, network, security |

### Concurrency Capacity

```
┌─────────────────────────────────────────────────────┐
│           CONCURRENT USER CAPACITY                  │
├─────────────────────────────────────────────────────┤
│                                                     │
│   3 gevent workers × 1,000 connections each         │
│   = ~3,000 simultaneous users                       │
│                                                     │
│   ✅ Hundreds at the same time?  EASY.             │
│   ✅ Thousands daily?            NO PROBLEM.       │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### PM2 Management Commands

```bash
pm2 list                    # View all processes
pm2 logs taskora            # Live log streaming
pm2 logs taskora --lines 50 # Last 50 log lines
pm2 restart taskora         # Manual restart
pm2 stop taskora            # Stop the app
pm2 monit                   # Real-time CPU/memory dashboard
pm2 save                    # Save current state
```

### Auto-Update on Code Changes

PM2 watches for file changes and **automatically restarts** when you update code:

- ✅ Watches: `.py`, `.html`, `.css`, `.js` files
- ❌ Ignores: `venv/`, `data/`, `__pycache__/`, `.git/`, uploads, logs

---

## 🎯 Core Concepts

### The Hierarchy

```
🏢 WORKSPACE (Organization)
 ├── 📁 PROJECT A
 │    ├── 📝 Issue WEB-1 (Task)
 │    ├── 🐛 Issue WEB-2 (Bug)
 │    └── 📖 Issue WEB-3 (Story)
 │
 ├── 📁 PROJECT B
 │    └── 🎯 Issue APP-1 (Epic)
 │
 ├── 👥 TEAM ALPHA
 │    ├── 👔 Team Lead: Alice
 │    ├── 💻 Dev: Bob
 │    └── 🧪 Tester: Charlie
 │
 └── 👥 TEAM BETA
      ├── 👔 Team Lead: Diana
      └── 💻 Dev: Eve
```

### Key Terms

| Term | Definition |
|------|-----------|
| **Workspace** | Isolated environment = your organization. Contains projects, teams, members. |
| **Project** | Collection of issues with a unique key (e.g., `WEB`, `API`). Has Kanban/Scrum board. |
| **Team** | Group of members. Can be invited to projects. Has a Team Lead. |
| **Issue** | Unit of work: Task, Bug, Story, or Epic. Has priority, status, assignee. |
| **Member** | User with a workspace role (Owner → Viewer). |

---

## 👥 Role System

Taskora uses a **dual-role system** — workspace roles + team roles:

### Workspace Roles (6 Levels)

```
👑 OWNER          Full control. Creator of the workspace. Cannot be removed.
    │
🛡️ ADMIN          Manages everything: members, projects, teams, roles.
    │
📋 PROJECT MGR    Creates/manages projects. Approves issues. Assigns teams.
    │
👔 TEAM MANAGER   Leads a team. Accepts project invitations. Assigns members.
    │
💻 DEVELOPER      Creates issues, works on tasks, participates in projects.
    │
👁️ VIEWER         Read-only. Sees everything but cannot create or modify.
```

### Team Roles (3 Levels)

| Role | Responsibility |
|------|---------------|
| **👔 Team Lead** | Full control over team operations, assigns issues to members |
| **💻 Developer** | Works on issues and tasks assigned by the team lead |
| **🧪 Tester** | Quality assurance, testing, and bug verification |

---

## 📊 Permissions Matrix

### Workspace-Level

| Action | 👑 Owner | 🛡️ Admin | 📋 PM | 👔 TM | 💻 Dev | 👁️ Viewer |
|--------|:--------:|:--------:|:-----:|:-----:|:------:|:---------:|
| View Dashboard | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| View Statistics | ✅ | ✅ | ❌ | ❌ | ❌ | ✅ |
| Create Projects | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |
| Create Teams | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Create Issues | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Invite Members | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Change Roles | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Delete Workspace | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |

### Project-Level

| Action | Owner/Admin | Project Manager | Team Lead | Dev | Viewer |
|--------|:-----------:|:---------------:|:---------:|:---:|:------:|
| View Board | ✅ | ✅ | ✅ | ✅ | ✅ |
| Edit Settings | ✅ | ✅ | ❌ | ❌ | ❌ |
| Invite Teams | ✅ | ✅ | ❌ | ❌ | ❌ |
| Approve Issues | ✅ | ✅ | ❌ | ❌ | ❌ |
| Create Subtasks | ✅ | ✅ | ❌ | ❌ | ❌ |

### Team-Level

| Action | Owner/Admin | Team Lead | Member | Non-Member | Viewer |
|--------|:-----------:|:---------:|:------:|:----------:|:------:|
| View Team | ✅ | ✅ | ✅ | ✅ | ✅ |
| Add Members | ✅ | ✅ | ❌ | ❌ | ❌ |
| Remove Members | ✅ | ✅ | ❌ | ❌ | ❌ |
| Accept Invitations | ✅ | ✅ | ❌ | ❌ | ❌ |
| Assign Issues | ✅ | ✅ | ❌ | ❌ | ❌ |

### Issue-Level

| Action | Owner/Admin | PM | Team Lead | Assignee | Others | Viewer |
|--------|:-----------:|:--:|:---------:|:--------:|:------:|:------:|
| View | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Create | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Edit | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Change Status | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Comment | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |

---

## 🏢 Workspaces

A **Workspace** is the top-level container — think of it as your organization or company.

### Workspace Isolation

Each workspace is **completely isolated**:
- 🔒 Members only see data within their workspace
- 🔄 Switching workspaces changes your entire view
- 👥 Users can belong to multiple workspaces
- 🚫 Data never leaks between workspaces

### Creating & Joining

```
┌────────────────────────────────────┐
│     How Users Join Workspaces      │
├────────────────────────────────────┤
│                                    │
│  Option 1: INVITATION              │
│  Admin sends invite → User accepts │
│                                    │
│  Option 2: JOIN REQUEST            │
│  User browses → Requests to join   │
│  → Admin approves → User joins     │
│                                    │
│  Option 3: ADMIN ADDS DIRECTLY     │
│  Admin → Members → Add User        │
│                                    │
└────────────────────────────────────┘
```

---

## 📁 Projects & Boards

### Project Features

- **Unique Key** — 2-4 letter code (e.g., `WEB`, `APP`) used as issue prefix
- **Board Type** — Kanban or Scrum
- **Project Manager** — Responsible person with full project control
- **Team Assignment** — Invite teams via a two-step acceptance process

### Kanban Board View

```
┌──────────────┬──────────────┬──────────────┬──────────────┐
│   BACKLOG    │ IN PROGRESS  │    REVIEW    │     DONE     │
├──────────────┼──────────────┼──────────────┼──────────────┤
│              │              │              │              │
│  ┌────────┐  │  ┌────────┐  │  ┌────────┐  │  ┌────────┐  │
│  │ WEB-1  │  │  │ WEB-3  │  │  │ WEB-5  │  │  │ WEB-2  │  │
│  │  Task  │  │  │  Bug   │  │  │ Story  │  │  │  Task  │  │
│  │ 🟡Med  │  │  │ 🔴Crit│  │  │ 🟠High│   │  │ 🟢Low │  │
│  └────────┘  │  └────────┘  │  └────────┘  │  └────────┘  │
│  ┌────────┐  │  ┌────────┐  │              │  ┌────────┐  │
│  │ WEB-4  │  │  │ WEB-6  │  │              │  │ WEB-7  │  │
│  │  Epic  │  │  │  Task  │  │              │  │  Bug   │  │
│  └────────┘  │  └────────┘  │              │  └────────┘  │
│              │              │              │              │
└──────────────┴──────────────┴──────────────┴──────────────┘
```

### Team-Project Assignment Flow

```
1. Project Manager invites a team to the project
                    ↓
2. Team Lead receives notification
                    ↓
3. Team Lead accepts or declines
                    ↓
4. If accepted → Team can now work on project issues
```

---

## 👥 Teams

### Team Structure

```
👥 Development Team
 ├── 👔 Team Lead: Alice       (manages team, assigns issues)
 ├── 💻 Developer: Bob         (works on features)
 ├── 💻 Developer: Charlie     (works on features)
 └── 🧪 Tester: Diana          (quality assurance)
```

### How to Join a Team

| Method | Process |
|--------|---------|
| **Request to Join** | Click "Request to Join" → Team Lead/Admin approves |
| **Added by Team Lead** | Team Lead adds member directly |
| **Added by Admin** | Workspace Admin adds member directly |

> ⚠️ **Note:** Team Leads cannot leave the team until replaced by an Admin.

---

## 📝 Issues & Workflow

### Issue Types

| Type | Icon | Description | Example |
|------|:----:|-------------|---------|
| **Task** | 📋 | General work item | "Add export to PDF feature" |
| **Bug** | 🐛 | Something broken | "Login fails on Safari" |
| **Story** | 📖 | User-facing feature | "As a user, I want to filter issues" |
| **Epic** | 🎯 | Large feature set | "User Authentication System" |

### Priority Levels

| Priority | Color | Response | Description |
|----------|:-----:|----------|-------------|
| **Critical** | 🔴 | Immediate | System down, data loss |
| **High** | 🟠 | Same day | Major feature broken |
| **Medium** | 🟡 | This week | Minor issues, improvements |
| **Low** | 🟢 | When free | Nice-to-have, cosmetic |

### Issue Lifecycle (Complete Flow)

```
                      ISSUE CREATION & APPROVAL FLOW
  ╔══════════════════════════════════════════════════════════════╗
  ║                                                              ║
  ║   Developer Creates Issue                                    ║
  ║          │                                                   ║
  ║          ▼                                                   ║
  ║   ┌─────────────────┐                                        ║
  ║   │ Pending Approval │  ◄── Issue starts here                ║
  ║   └────────┬────────┘                                        ║
  ║            │                                                 ║
  ║            ▼                                                 ║
  ║   Project Manager Reviews                                    ║
  ║            │                                                 ║
  ║      ┌─────┴─────┐                                           ║
  ║      ▼           ▼                                           ║
  ║  ┌────────┐  ┌────────┐                                      ║
  ║  │APPROVE │  │ DENY   │──► Creator notified                  ║
  ║  └───┬────┘  └────────┘                                      ║
  ║      │                                                       ║
  ║      ▼                                                       ║
  ║  PM Assigns to Team                                          ║
  ║      │                                                       ║
  ║      ▼                                                       ║
  ║  Team Lead Accepts                                           ║
  ║      │                                                       ║
  ║      ▼                                                       ║
  ║  Team Lead Assigns Members                                   ║
  ║      │                                                       ║
  ║      ▼                                                       ║
  ║   STATUS FLOW:                                               ║
  ║   ┌────────┐  ┌────────────┐  ┌────────┐  ┌──────┐           ║
  ║   │BACKLOG │─▶│IN PROGRESS │─▶│ REVIEW │─▶│ DONE │         ║
  ║   └────────┘  └────────────┘  └────────┘  └──────┘           ║
  ║       ▲                                        │             ║
  ║       └────────────────────────────────────────┘             ║
  ║              (Can move to any status)                        ║
  ║                                                              ║
  ╚══════════════════════════════════════════════════════════════╝
```

> 💡 **Shortcut:** Admins and Project Managers can create issues that **bypass** the approval workflow.

---

## 🤖 AI Assistant

Taskora includes a **context-aware AI assistant** powered by **Google Gemini** with multi-key rotation for high availability.

### Features

| Feature | Description |
|---------|-------------|
| **Context-Aware** | Knows your projects, teams, issues, and role |
| **Natural Language** | Ask questions in plain English |
| **Multi-Key Rotation** | Up to 10 API keys with automatic failover |
| **Privacy-First** | Only accesses YOUR data. Never stores externally |
| **Session Memory** | Remembers conversation context |

### What You Can Ask

```
💬 "What projects am I working on?"
💬 "Show my high-priority issues"
💬 "What's my completion rate?"
💬 "Which teams am I part of?"
💬 "Give me a summary of my overdue tasks"
💬 "Who is the lead of Team Alpha?"
```

### How to Access

- Click the **purple AI button** (bottom-right corner)
- Or press **`Ctrl/Cmd + K`**

### AI Modules

| Module | File | Purpose |
|--------|------|---------|
| **Gemini Client** | `gemini_client.py` | API communication with key rotation |
| **Context Builder** | `context_builder.py` | Builds user-specific context for AI |
| **Chat Manager** | `chat_manager.py` | Manages conversation flow |
| **Memory Store** | `memory_store.py` | Session-based conversation memory |
| **Prompts** | `prompts.py` | System prompts and templates |
| **AI Routes** | `routes/ai_routes.py` | Flask API endpoints for AI |

---

## 💬 Messaging & Notifications

### Communication Channels

| Channel | Description | Who Can Access |
|---------|-------------|---------------|
| **📩 Direct Messages** | One-on-one conversations | Any two workspace members |
| **🏠 Workspace Chat** | General workspace discussion | All workspace members |
| **👥 Group Chats** | Topic-specific group conversations | Group members only |

### Notification System

Non-blocking **slide-in toast notifications** that auto-dismiss after 4 seconds:
- 🔔 New join requests
- ✅ Request approved/rejected
- 📋 Issue assignments
- 💬 New messages
- 📨 Team/project invitations
- 🔄 PM/TL transfer requests (Accept/Decline from inbox)

---

## 🔄 PM/TL Transfer System

Taskora supports **role transfer workflows** for Project Managers and Team Leaders:

### How It Works

```
┌────────────────────────────────────────────────────────┐
│              PM / TL TRANSFER FLOW                     │
├────────────────────────────────────────────────────────┤
│                                                        │
│  🛡️ ADMIN initiates transfer                          │
│     → Instantly changes role                           │
│     → Both parties notified                            │
│                                                        │
│  📋 PM / 👔 TL initiates transfer                     │
│     → Candidate receives notification                  │
│     → Candidate sees Accept / Decline buttons          │
│     → If accepted: role transfers immediately          │
│     → If declined: requester notified, nothing changes │
│                                                        │
└────────────────────────────────────────────────────────┘
```

### Transfer Endpoints

| Route | Method | Description |
|-------|--------|-------------|
| `/workspace/<ws>/transfer-pm/<proj>` | POST | Initiate PM transfer |
| `/workspace/<ws>/transfer-tl/<team>` | POST | Initiate TL transfer |
| `/transfer/accept/<notification>` | POST | Accept transfer request |
| `/transfer/decline/<notification>` | POST | Decline transfer request |

---

## ⚡ Super Admin Panel

The **Super Admin Panel** provides system-wide control over all users, workspaces, teams, and projects from a single command center.

### Dashboard Tabs

| Tab | Features |
|-----|----------|
| **👤 Users** | View all users, change roles, More Info link, delete with safe cascading |
| **🏢 Workspaces** | View all workspaces, owner info, delete workspace |
| **👥 Teams** | View all teams, leader, member count, status, More Info link |
| **📁 Projects** | View all projects, PM, team count, issue count, status |

### Smart Search

Global search bar filters **all tables in all tabs** in real-time with result count.

### User Detail Page (`/super-admin/user/<id>`)

- Editable: display name, profile image (file upload), role, bio
- Read-only: email, gender, join date
- Tables: workspaces, teams (linked to team detail), projects, issues
- **Profile image upload**: admin can upload a new image for any user (old image auto-deleted)
- **Change notifications**: user receives a notification listing every field changed with old → new values
- **Deletion guard**: cannot delete a user who is a Team Leader or Project Manager — roles must be reassigned first

### Team Detail Page (`/super-admin/team/<id>`)

- Editable: name, description, status, team leader (dropdown)
- Tables: members (with links to user detail), projects, issues
- Change team leader with automatic role reassignment

---

## 📈 Statistics & Reporting

**Access:** Admin and Viewer roles only

### Overview Dashboard

| Metric | Description |
|--------|-------------|
| Total Members | Number of users in workspace |
| Total Teams | Number of active teams |
| Total Projects | Number of projects |
| Total Issues | All issues across projects |
| Completed | Issues marked as Done |
| Overdue | Past due date, not done |
| Completion Rate | (Completed / Total) × 100% |

### Statistics Tabs

| Tab | Shows |
|-----|-------|
| **👤 User Stats** | Per-user breakdown: issues total, completed, in progress, overdue, completion % |
| **👥 Team Stats** | Per-team cards: member count, issue breakdown, completion rate |
| **⚠️ Overdue** | All overdue issues with details |

**Filtering:** By team, by project  
**Pagination:** 10 users/page with navigation

---

## 🌗 Dark Mode

Taskora includes a premium dark mode with:
- 🎨 Carefully crafted dark color palette
- 🔄 One-click toggle
- 💾 Preference saved per user
- 📄 27,500+ lines of dark theme CSS

---

## 📚 Documentation Portal

Built-in documentation portal with **bilingual support**:

| Topic | English | Arabic |
|-------|:-------:|:------:|
| Roles & Permissions | ✅ `roles_en.html` | ✅ `roles_ar.html` |
| Workspaces | ✅ `workspaces_en.html` | ✅ `workspaces_ar.html` |
| Projects | ✅ `projects_en.html` | ✅ `projects_ar.html` |
| Teams | ✅ `teams_en.html` | ✅ `teams_ar.html` |
| Issues | ✅ `issues_en.html` | ✅ `issues_ar.html` |
| Workflow | ✅ `workflow_en.html` | ✅ `workflow_ar.html` |
| Statistics | ✅ `statistics_en.html` | ✅ `statistics_ar.html` |

---

## 🌐 Environment Variables

Create a `.env` file from `.env.example`:

| Variable | Description | Required | Default |
|----------|-------------|:--------:|---------|
| `SECRET_KEY` | Flask session encryption key | ✅ | Dev key (change in prod!) |
| `GEMINI_API_KEY` | Primary Google Gemini API key | For AI | — |
| `GEMINI_API_KEY_1` to `_10` | Failover API keys for rotation | Optional | — |
| `AI_ENABLED` | Enable/disable AI assistant | No | `true` |
| `AI_MAX_CONTEXT_MESSAGES` | Conversation memory depth | No | `10` |
| `AI_RESPONSE_TEMPERATURE` | AI creativity (0.0–1.0) | No | `0.7` |
| `ELASTICSEARCH_URL` | Elasticsearch connection URL | No | `http://localhost:9200` |
| `PORT` | Server port | No | `5000` |

---

## 📂 Project Structure

```
taskora/
├── 📄 app.py                      # Main Flask application (~5,700+ lines)
├── 📄 gunicorn.conf.py            # Gunicorn production config
├── 📄 ecosystem.config.js         # PM2 process manager config
├── 📄 requirements.txt            # Python dependencies
├── 📄 .env.example                # Environment variables template
├── 📄 migrate_json_to_es.py       # JSON → Elasticsearch migration tool
│
├── 🔐 auth_users.py              # Authentication system (register, login, sessions)
├── 🏢 workspaces.py               # Workspace management & isolation
├── 📁 projects.py                 # Project CRUD & board management
├── 👥 teams.py                    # Team management & membership
├── 📝 issues.py                   # Issue lifecycle & tracking
├── 📋 issue_requests.py           # Issue approval workflow
├── 💬 messages.py                 # Messaging system
├── 🔔 notifications.py           # Notification system
├── 💬 comments.py                 # Issue comments
├── 📈 progress.py                 # Progress tracking & statistics
├── 👤 users.py                    # User management
├── 🔍 storage.py                  # Elasticsearch storage engine
├── 👥 group_manager.py            # Group chat management
│
├── 🤖 ai_assistant/              # AI Assistant Module
│   ├── __init__.py
│   ├── gemini_client.py           # Gemini API client with key rotation
│   ├── context_builder.py         # User context builder
│   ├── chat_manager.py            # Conversation manager
│   ├── memory_store.py            # Session memory
│   └── prompts.py                 # AI system prompts
│
├── 🛣️ routes/                     # Modular route blueprints
│   ├── ai_routes.py               # AI assistant API endpoints
│   └── group_routes.py            # Group chat routes
│
├── 🎨 static/
│   ├── css/
│   │   ├── ai_assistant.css       # AI widget styles
│   │   └── dark-mode.css          # Dark theme (27,500 lines)
│   ├── js/
│   │   ├── ai_assistant.js        # AI widget logic
│   │   └── dark-mode.js           # Dark mode toggle
│   ├── imags/                     # App assets (favicon, AI icons)
│   └── profile/                   # User profile images
│
└── 📄 templates/                  # 61 Jinja2 HTML templates
    ├── base.html                  # Base template with nav
    ├── dashboard.html             # Main dashboard
    ├── login.html / register.html # Premium auth forms
    ├── projects.html              # Projects list
    ├── project_board.html         # Kanban/Scrum board
    ├── teams.html                 # Teams list
    ├── issues.html                # Issues list
    ├── workspace_statistics.html  # Analytics dashboard
    ├── docs/                      # 14 bilingual doc pages (EN/AR)
    ├── groups/                    # Group chat templates
    └── components/                # Reusable components
```

---

## ❓ FAQ

<details>
<summary><b>Can I use Taskora offline?</b></summary>

Everything except the AI Assistant works offline as long as Elasticsearch is running locally. All data is stored in your local Elasticsearch instance — nothing is sent to the cloud.
</details>

<details>
<summary><b>How many users can it handle?</b></summary>

With the current production setup (3 gevent workers), Taskora can handle **~3,000 simultaneous users** and thousands of daily users.
</details>

<details>
<summary><b>Is my data secure?</b></summary>

Yes. All data is stored in Elasticsearch running on `localhost` only — it's not exposed to the internet. Nothing is sent externally except AI queries (and those don't include sensitive personal data).
</details>

<details>
<summary><b>Can a user have multiple roles?</b></summary>

Yes! A user can be a Developer at workspace level and a Team Lead at team level.
</details>

<details>
<summary><b>Can Viewers create anything?</b></summary>

No. Viewers have strictly read-only access. They cannot create, edit, or delete anything.
</details>

<details>
<summary><b>Can a team work on multiple projects?</b></summary>

Yes! Teams can be invited to any number of projects.
</details>

<details>
<summary><b>What happens when I create an issue?</b></summary>

It enters "Pending Approval" status. The Project Manager must approve it before work begins. Admins and PMs can bypass this step.
</details>

<details>
<summary><b>Does it restart automatically after a server reboot?</b></summary>

Yes! PM2 with systemd startup ensures all apps (including Taskora) automatically restart on server reboot.
</details>

<details>
<summary><b>Does it auto-update when I change code?</b></summary>

Yes! PM2 file watching detects changes to `.py`, `.html`, `.css`, and `.js` files and automatically restarts the server.
</details>

---

## 🔧 Troubleshooting

| Problem | Solution |
|---------|----------|
| Can't log in | Verify email is registered. Check password (min 8 chars). |
| Can't see workspace | Request to join or get invited by an admin. |
| Can't create issues | You might be a Viewer (read-only). Ask admin for Developer role. |
| AI not responding | Check API keys in `.env`. Verify `AI_ENABLED=true`. |
| Page not loading | Run `pm2 logs taskora` to check for errors. |
| Elasticsearch not connecting | Run `curl http://localhost:9200` to verify. Start with `sudo systemctl start elasticsearch`. |
| Port already in use | Check `ss -tlnp | grep 5000` and stop conflicting process. |
| PM2 not starting on boot | Run `pm2 startup` and execute the sudo command it provides. |
| ES out of memory | Edit `/etc/elasticsearch/jvm.options.d/taskora.options` and adjust `-Xms`/`-Xmx`. |

---

## 📜 Changelog

| Version | Date | Highlights |
|---------|------|------------|
| **5.0.0** | Feb 2026 | ⚡ **Super Admin Panel** — user/team detail pages, smart search, projects tab, safe deletion, PM/TL transfer system, toast notifications |
| **4.0.0** | Feb 2026 | 🔍 **Elasticsearch migration** — replaced JSON file storage with ES 8.x for speed, stability & security. Removed 14 unused scripts. |
| **3.0.0** | Feb 2026 | 🚀 Production deployment (Gunicorn + gevent + PM2), 3K concurrent users, auto-restart, file watching |
| **2.5.0** | Feb 2026 | 📱 Mobile-first redesign, premium auth forms, group chat, sorting & filtering |
| **2.0.0** | Dec 2025 | 👁️ Viewer role, Statistics page, workspace data isolation, enhanced permissions |
| **1.5.0** | Dec 2025 | 🤖 AI Assistant with Gemini, multi-key rotation, context-aware responses |
| **1.0.0** | Oct 2025 | 🎉 Initial release — workspaces, projects, teams, issues, messaging |

---

## 🤝 Contributing

> ⚠️ **This is proprietary software.** Contributions, forks, and pull requests are **not accepted**.
>
> If you are interested in licensing, collaboration, or partnership opportunities, please [contact the author](mailto:alaadinalynaey@gmail.com).

---

## 📄 License

**© 2024-2026 Alaadin Alynaey. All Rights Reserved.**

This software is **proprietary and confidential**. Unauthorized copying, modification, distribution, or any use of this software is **strictly prohibited** and may result in civil and criminal penalties.

See the [LICENSE](LICENSE) file for the complete terms.

> **Prohibited:** Copying · Forking · Modifying · Distributing · Commercial Use · Personal Use · AI Training · Code Extraction

---

<div align="center">

<br>

### ⚡ Built with passion. Designed for productivity.

**[Taskora](https://github.com/AladdinAlynaey/taskora)** — _Because great teams deserve great tools._

<br>

Made by **AI Eng. Aladdin Alynaey**

[⬆ Back to Top](#-taskora)

</div>
