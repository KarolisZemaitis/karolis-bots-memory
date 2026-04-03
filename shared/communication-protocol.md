# Bot Fleet Communication Protocol (Hybrid)

## Overview
The bot fleet uses a hybrid communication approach combining git-based inbox files (for history & memory) with RemoteTrigger (for instant execution). Chief of Staff Bot is the central coordinator.

## How It Works

### 1. Task Assignment (Git Inbox)
- The orchestrator (Chief of Staff or Assistant Bot) writes a task file to the target bot's `inbox/` folder
- Filename format: `from-SENDER-YYYY-MM-DD-subject.md`
- The file contains: task description, urgency, expected response format, deadline
- Orchestrator commits and pushes: `git add -A && git commit -m "BOT: description" && git push`

### 2. Instant Wake-Up (RemoteTrigger or Cron)
- After pushing the task file, the orchestrator triggers the target bot to wake up
- The target bot's startup/cron prompt includes: `git pull` then check `inbox/` for new tasks
- This ensures instant execution without polling delays

### 3. Task Execution & Response
- Target bot pulls latest, finds the task file in `inbox/`
- Executes the task
- Writes a response file to the requesting bot's inbox: `../REQUESTER/inbox/from-BOTNAME-YYYY-MM-DD-subject.md`
- Moves the original task file to `inbox/processed/`
- Commits and pushes all changes

### 4. Result Pickup
- The orchestrator picks up the response on its next inbox check
- Notifies Karolis on Telegram with the result summary

## Task File Format

```markdown
# Task: [Short Title]

**From:** [Sender Bot Name]
**Date:** YYYY-MM-DD
**Urgency:** 🔴 Critical / 🟡 Important / 🟢 FYI

## Instructions
[Clear description of what needs to be done]

## Expected Response
[What the response file should contain]

## Deadline
[ASAP / specific time / end of day]
```

## Response File Format

```markdown
# [Task Title] — Completed

**From:** [Responder Bot Name]
**Date:** YYYY-MM-DD
**Status:** ✅ Done / ❌ Failed / ⏳ In Progress

## Summary
[What was done, key results]

## Details
[Links, data, or additional context]
```

## Shared Knowledge
- `../shared/` contains info all bots can read: team info, contacts, processes, this protocol
- If a bot learns something all bots should know, update `../shared/`
- Each bot maintains its own memory in its working directory

## Git Rules
- Always `git pull` before checking inbox or writing files
- Always commit and push after any file changes
- Commit message format: `bot-name: short description`
- If a push fails (conflict), pull with rebase and retry: `git pull --rebase && git push`

## Orchestrators
- **Chief of Staff Bot** — primary coordinator, delegates to all bots
- **Assistant Bot** — secondary orchestrator, can delegate simple tasks

## Bot Registry
| Bot | Directory | Role |
|-----|-----------|------|
| Chief of Staff | /chief-of-staff-bot | Coordinator & strategic advisor |
| Briefing Bot | /briefing-bot | Daily briefings & monitoring |
| Assistant Bot | /assistant-bot | Daily tasks & knowledge help |
| Insurance Detector | /auto-fraud-discovery | Auto insurance fraud research |
