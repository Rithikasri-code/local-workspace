<p align="center">
  <img src="assets/banner.svg" alt="Local Workspace Banner" width="100%" />
</p>

<p align="center">
  <a href="https://github.com/Rithikasri-code/workspace"><img src="https://img.shields.io/badge/Standard-AGENTS.md-a855f7?style=flat-square&logo=markdown&logoColor=white&labelColor=0f172a" alt="AGENTS.md" /></a>
  <img src="https://img.shields.io/badge/Storage-Plain%20Markdown-6366f1?style=flat-square&labelColor=0f172a" alt="Markdown Store" />
  <img src="https://img.shields.io/badge/Browser%20API-File%20System%20Access-38bdf8?style=flat-square&labelColor=0f172a" alt="File System Access" />
  <img src="https://img.shields.io/badge/Privacy-100%25%20Local--First-22c55e?style=flat-square&labelColor=0f172a" alt="Local-First" />
  <img src="https://img.shields.io/badge/Agents-Claude%20%7C%20Codex%20%7C%20Antigravity%20%7C%20Cursor-818cf8?style=flat-square&labelColor=0f172a" alt="Multi-Agent" />
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square&labelColor=0f172a" alt="MIT License" /></a>
</p>

---

## ⚡ Overview

**Workspace** is an agent-native personal operating system and task management architecture where **plain Markdown files** on your computer serve as the verifiable, version-controlled single source of truth.

Instead of locking task metadata, goals, and daily plans into proprietary SaaS silos, Workspace enables autonomous AI agents (**Claude Code**, **Codex**, **Antigravity**, **Cursor**) to read, organize, plan, and update your workspace through natural conversation, while a zero-dependency **live browser dashboard** provides real-time visualization via the Chromium **File System Access API**.

---

## 🏗️ Architecture & Interaction Flow

```mermaid
flowchart TD
    subgraph AgentLayer["🤖 Autonomous AI Agents"]
        Claude["Claude Code / Terminal"]
        Cursor["Cursor / Copilot / Codex"]
        AGY["Antigravity / Gemini CLI"]
    end

    subgraph FileStore["📁 Plain-Text Markdown Single Source of Truth"]
        Tasks["tasks.md\n(Kanban Statuses, Deadlines, Estimations)"]
        Goals["goals.md\n(Objectives & Completion Progress)"]
        Daily["daily/YYYY-MM-DD.md\n(Morning Plans, Worklogs, Retrospectives)"]
        Memory["memory/\n(Long-term Learnings & Ingested Facts)"]
    end

    subgraph Dashboard["🖥️ Local Workspace Client"]
        FSA["File System Access API\n(Native Local Directory Handle)"]
        LivePoller["1.5s Reactive Change Poller\n(Conflict-Free Hot Reloading)"]
        Kanban["Interactive Board\n(Inbox · Next · Doing · Waiting · Done)"]
    end

    AgentLayer <-->|"Reads/Writes via AGENTS.md Protocol"| FileStore
    FileStore <-->|"Bidirectional Sync via Local File API"| FSA
    FSA --> LivePoller
    LivePoller --> Kanban
```

---

## 🚀 Core Architectural Capabilities

### 1. **Agent-Native Standard Protocol (`AGENTS.md`)**
The behavior, file conventions, syntax grammar, and task rollover rules are codified directly in [`AGENTS.md`](AGENTS.md) and [`.agents/skills/`](.agents/skills), adhering to the open **Agent Skills** specification. Any coding agent instantly understands how to parse and edit your workspace without custom API servers.

### 2. **File System Access API (Zero Cloud Lock-in)**
The dashboard connects directly to your local file system folder using modern browser File System Access APIs. No web servers, no databases, no cloud authentication, and no data telemetry.

### 3. **Conflict-Free Reactive Hot Reloading**
The client monitors file timestamps every 1.5 seconds. If an autonomous agent completes tasks in the background, the visual Kanban board and goal metrics update smoothly without overwriting in-flight user edits.

### 4. **Selective Memory & Ingestion Subsystem (`ingest`)**
Includes automated ingestion procedures that filter noise from communication channels (Slack, GitHub PRs, meeting notes) into clean, actionable task cards.

---

## 🔄 Daily Workflow Matrix

| Phase | What you tell your Agent | Real-time Dashboard Reflection |
| :--- | :--- | :--- |
| **Capture** | *"capture: review payment protocol PR"* | Instantly creates a card in `Inbox` |
| **Morning** | *"plan the day"* | Selects Top 3 priorities, moves to `Doing`, generates `daily/` log |
| **Execution** | *"sent PR for review, blocked on CI"* | Automatically shifts card to `Waiting` |
| **Wrap-up** | *"/capture"* | Extracts key architectural decisions into `memory/` |
| **Shutdown** | *"shut down the day"* | Marks completed items, drafts tomorrow's `Next` column |

---

## 💻 Quickstart

### Option 1: Instant Browser Access (Recommended)
Open any Chromium-based browser (Chrome, Edge, Brave, Arc) and load [`index.html`](index.html):
```bash
# Serve locally with Python:
python scripts/app.py
```
1. Click **Open Folder**.
2. Select your `workspace` repository root.
3. Grant read/write permission to begin real-time tracking.

### Option 2: Connecting Your AI Agent
* **Antigravity / Cursor / Codex:** Open the folder directly—the agent will automatically detect and parse `AGENTS.md`.
* **Claude Code:** Run the initialization helper:
  ```bash
  python scripts/setup.py
  ```

---

## 📂 Vault Structure

```
├── AGENTS.md              # Machine-readable instructions for autonomous agents
├── tasks.md               # Primary task board (Inbox, Next, Doing, Waiting, Done)
├── goals.md               # High-level strategic goals with metric tracking
├── daily/                 # Day-by-day notes and plans (YYYY-MM-DD.md)
├── memory/                # Durable knowledge base and confirmed learnings
├── projects/              # Detailed project briefs and architecture records
├── app/                   # Single-page zero-dependency dashboard
└── scripts/               # Developer automation scripts (app.py, setup.py)
```

---

## 📄 License

Distributed under the **MIT License**. See [LICENSE](LICENSE) for details.
