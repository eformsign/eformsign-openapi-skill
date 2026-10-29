# eformsign Open API Skill — Installation Guide

## What Is This?

The **eformsign Open API Skill** is an **Agent Skill** that makes AI coding assistants expert helpers for integrating the [eformsign](https://www.eformsign.com) electronic document service. The skill provides accurate reference material for the REST API, iframe embedding, webhook handling, and MCP connection — including known server quirks and undocumented fields not in the official docs.

Agent Skills is an open standard supported by multiple AI clients (Claude Code, Cursor, and others).

---

## What Is Included?

The **eformsign Open API Skill** is a single skill file, `eformsign.skill`, and covers everything:

- Document APIs, embedding, webhook, and an MCP connection guide
- Organization management APIs (templates, members, groups, seals) — these require **administrator permission**

> **Upgrading from `eformsign-user.skill`?** It has been merged into `eformsign.skill`. Delete the `eformsign-user` folder from your skills directory, then install `eformsign.skill`.

---

## Supported Clients

| Client | Tested | Global install path |
|--------|--------|---------------------|
| **Claude Code** | ✅ | `~/.claude/skills/` |
| **Claude Desktop + claude.ai** | ✅ | UI-based (Settings > Customize > Skills) |
| **Cursor** | ✅ | `~/.cursor/skills/` |
| **GitHub Copilot** (VS Code) | ✅ | `~/.copilot/skills/` |
| **Google Antigravity** (desktop + `agy` CLI) | ✅ | `~/.gemini/config/skills/` |
| **Codex CLI** (`codex`) | ✅ | `~/.codex/skills/` |
| **Cline** (VS Code) | ✅ | `~/.cline/skills/` |
| **ChatGPT** (web/app) | ❌ Business+ plan required | UI-based, not file-system |

> **Tip:** GitHub Copilot also recognizes `~/.claude/skills/` as a valid skill path. If you already installed the skill for Claude Code, GitHub Copilot may pick it up automatically without a separate installation.

---

## Installation

Download the `.skill` file(s) from the [`dist/`](dist/) folder in this repository.

### Claude Code

#### macOS / Linux

```bash
mkdir -p ~/.claude/skills
cd ~/.claude/skills
unzip /path/to/eformsign.skill
```

#### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills"
cd "$env:USERPROFILE\.claude\skills"
Expand-Archive -Force "C:\path\to\eformsign.skill" .
```

After installation, **start a new Claude Code session** — skills are loaded at session startup.

---

### Claude Desktop + claude.ai

1. Open **Settings > Customize > Skills > Add > Create Skill > Upload Skill**
2. Select the `.skill` file from the [`dist/`](dist/) folder
3. Confirm — the skill name and description are displayed automatically

No file path setup needed. The skill is auto-invoked based on conversation context. Available on Free, Plus, Pro, and Max plans.

> **Skills are synced across your Anthropic account** — a skill installed in Claude Desktop is automatically available in claude.ai, and vice versa. One installation covers both.

---

### GitHub Copilot (VS Code)

#### macOS / Linux

```bash
mkdir -p ~/.copilot/skills
cd ~/.copilot/skills
unzip /path/to/eformsign.skill
```

#### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.copilot\skills"
cd "$env:USERPROFILE\.copilot\skills"
Expand-Archive -Force "C:\path\to\eformsign.skill" .
```

> **Already have Claude Code?** Skip this step — GitHub Copilot also scans `~/.claude/skills/`, so the skill installed there works for both clients.

To add custom paths, open VS Code settings and add to `chat.agentSkillsLocations`.

After installation, **reload VS Code** (or open a new Copilot Chat session).

---

### Cursor

#### macOS / Linux

```bash
mkdir -p ~/.cursor/skills
cd ~/.cursor/skills
unzip /path/to/eformsign.skill
```

#### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.cursor\skills"
cd "$env:USERPROFILE\.cursor\skills"
Expand-Archive -Force "C:\path\to\eformsign.skill" .
```

> **⚠️ Important:** Do **not** place files under `~/.cursor/skills-cursor/`. That directory is reserved for Cursor's internal built-in skills and is managed automatically — user skills placed there will be ignored or overwritten.

After installation, **restart Cursor** — skills are loaded at startup.

---

### Google Antigravity (desktop + `agy` CLI)

#### macOS / Linux

```bash
mkdir -p ~/.gemini/config/skills
cd ~/.gemini/config/skills
unzip /path/to/eformsign.skill
```

#### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.gemini\config\skills"
cd "$env:USERPROFILE\.gemini\config\skills"
Expand-Archive -Force "C:\path\to\eformsign.skill" .
```

After installation, restart Antigravity or open a new session. The skill is auto-invoked — no explicit call syntax needed.

---

### Codex CLI

#### macOS / Linux

```bash
mkdir -p ~/.codex/skills
cd ~/.codex/skills
unzip /path/to/eformsign.skill
```

#### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills"
cd "$env:USERPROFILE\.codex\skills"
Expand-Archive -Force "C:\path\to\eformsign.skill" .
```

> Skills installed to `~/.codex/skills/` are also available in the Codex desktop app and IDE extension — one installation covers all Codex surfaces.

After installation, start a new `codex` session.

---

### Cline (VS Code)

#### macOS / Linux

```bash
mkdir -p ~/.cline/skills
cd ~/.cline/skills
unzip /path/to/eformsign.skill
```

#### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.cline\skills"
cd "$env:USERPROFILE\.cline\skills"
Expand-Archive -Force "C:\path\to\eformsign.skill" .
```

After installation, open the Cline panel in VS Code, click the **⚖️ icon** (bottom of panel), and verify the skill appears in the Skills tab. Enable it if not already active.

---

### Cross-platform (Python — works for any client)

```python
import zipfile, os

skill_file = "eformsign.skill"

# Change the path below to match your client:
#   Claude Code        → os.path.join(os.path.expanduser("~"), ".claude", "skills")
#   Cursor             → os.path.join(os.path.expanduser("~"), ".cursor", "skills")
#   GitHub Copilot     → os.path.join(os.path.expanduser("~"), ".copilot", "skills")
#   Google Antigravity → os.path.join(os.path.expanduser("~"), ".gemini", "config", "skills")
#   Codex CLI          → os.path.join(os.path.expanduser("~"), ".codex", "skills")
#   Cline              → os.path.join(os.path.expanduser("~"), ".cline", "skills")
install_dir = os.path.join(os.path.expanduser("~"), ".claude", "skills")

os.makedirs(install_dir, exist_ok=True)
with zipfile.ZipFile(skill_file, "r") as z:
    z.extractall(install_dir)

print(f"Installed to {install_dir}")
```

---

## Verify & Use

### Claude Code

In a new session, just describe your task — Claude automatically loads the skill when it detects an eformsign-related request:

```
Write Python code to issue an eformsign access token using the eformsign signature method.
```

To confirm the skill is loaded, ask:
```
What eformsign skills do you have available?
```

### Claude Desktop + claude.ai

Just describe your task — the skill is loaded automatically on both surfaces:

```
Write Python code to issue an eformsign access token using the eformsign signature method.
```

### GitHub Copilot (VS Code)

Open **Copilot Chat** in VS Code in **Agent mode** and invoke the skill with `/`:

```
/eformsign Write Python code to issue an eformsign access token using the eformsign signature method.
```

> Typing `/` in Copilot Chat shows available skills — select `eformsign` from the list or type the full name.

### Cursor

Open **Agent mode** (`Ctrl+I` / `Cmd+I`) and describe your task. The skill is loaded automatically based on the description:

```
eformsign API로 access token 발급하는 Python 코드 작성해줘
```

To invoke explicitly, prefix with `@`:

```
@eformsign How do I embed eformsign document signing for an external user?
```

### Cline (VS Code)

Just describe your task — the skill is loaded automatically:

```
Write Python code to issue an eformsign access token using the eformsign signature method.
```

### Google Antigravity

**Desktop app:** Just describe your task — the skill is loaded automatically via semantic matching:

```
Write Python code to issue an eformsign access token using the eformsign signature method.
```

**CLI (`agy`):** Works the same way from the terminal:

```bash
agy "Write Python code to issue an eformsign access token using the eformsign signature method."
```

Or start an interactive session:

```bash
agy
```

---

## Example Prompts

**API integration:**
```
Write Python code to issue an eformsign access token using the eformsign signature method.
```

**Embedding:**
```
How do I embed eformsign document signing into my React page for an external (non-member) user?
```

**Webhook:**
```
Set up a Node.js Express server to receive eformsign webhook events and verify the signature.
```

**Document operations:**
```
Show me how to create a document via the eformsign API and then download the PDF after it's completed.
```

---

## Client Differences

| | Claude Code | Claude Desktop / claude.ai | GitHub Copilot | Cursor | Cline | Google Antigravity | Codex CLI |
|--|-------------|---------------------------|----------------|--------|-------|--------------------|-----------|
| Install path | `~/.claude/skills/` | UI upload (account-synced) | `~/.copilot/skills/` | `~/.cursor/skills/` | `~/.cline/skills/` | `~/.gemini/config/skills/` | `~/.codex/skills/` |
| Also scans | — | — | `~/.claude/skills/` ✓ | — | — | — | — |
| Project path | `.claude/skills/` | — | `.github/skills/` | `.cursor/skills/` | `.cline/skills/` | `.agents/skills/` | `.codex/skills/` |
| Auto-invocation | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ (semantic matching) | ✅ |
| Explicit invocation | — | — | ✅ `/eformsign` | `@eformsign` | — | — | — |
| CLI support | ✅ | — | — | — | — | ✅ `agy` | ✅ `codex` |
| `disable-model-invocation` | Not supported | Not supported | Supported | Supported | Unknown | Unknown | Unknown |
| Note | — | Free/Plus/Pro/Max; Desktop ↔ claude.ai synced | Skill description must be broad enough | — | Enable via ⚖️ icon → Skills tab | Free in public preview | Also works in Codex app + IDE |
| Extra config | — | — | `chat.agentSkillsLocations` | — | — | — | — |

### What is `disable-model-invocation`?

A SKILL.md frontmatter field specific to Cursor that controls how the skill is triggered:

| Value | Behavior |
|-------|----------|
| Not set (default) | AI automatically loads the skill when it detects a relevant task |
| `true` | AI **never** auto-loads the skill — user must call it explicitly with `@eformsign` |

Cursor recommends `true` as the default to prevent unnecessary skill loading when many skills are installed. The eformsign skill does not set this field, so it uses auto-invocation (same as Claude Code behavior). If the skill is triggered in unintended situations, add `disable-model-invocation: true` to the SKILL.md frontmatter.

---

## What the Skill Covers

| Area | Details |
|------|---------|
| **Authentication** | Access Token issuance (Bearer / Basic / eformsign Signature), Refresh Token renewal |
| **Document API** | Create, list, get, download PDF, delete, cancel, decline, bulk send, re-request |
| **Org Management** | Templates, members, groups, company seals (administrator permission required) |
| **Embedding** | Script loading, `EformSignDocument` / `EformSignTemplate` SDK, `document_option` config, callbacks |
| **Webhook** | Event structure, signature verification, server examples (Python/Node.js) |
| **MCP** | How to connect to the eformsign-hosted MCP server (OAuth). Ask your company administrator for the client ID/secret |
| **Code Examples** | Language-specific examples in Python, JavaScript/Node.js, Java, PHP, C# |

### Known issues documented

| ID | Category | Issue |
|----|----------|-------|
| BUG-01 | API path | `GET /api/list_documents` (plural) → must use `/api/list_document` (singular) |
| BUG-02 | Server behavior | `limit` field is documented as optional but omitting it returns an empty list |
| BUG-03 | SDK bug | Global constant collision when `efs_embedded_v2.js` and `efs_embedded_form.js` are both loaded |
| BUG-04 | Server behavior | `PATCH /api/members`: `account.contact` is effectively required (error 4000070) |
| BUG-05 | SDK undocumented | `user.auth_id` is required for external users — omitting it redirects to the login page |
| BUG-06 | Server behavior | `PATCH /api/groups`: `group.description` is effectively required (error 4000001) |

---

## Updating the Skill

Re-download the latest `.skill` file and repeat the installation steps. The new files will overwrite the previous version.

---

## Supported Languages

Python · JavaScript/Node.js · Java · PHP · C#
