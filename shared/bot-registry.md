# Bot Registry

## Active Bots

| Bot Name | Directory | Purpose |
|----------|-----------|---------|
| Chief of Staff | /chief-of-staff-bot | Fleet coordinator, strategic advisor |
| Briefing Bot | /briefing-bot | Daily morning briefings |
| Assistant Bot | /assistant-bot | Daily tasks, knowledge help |
| Auto Fraud Discovery | /auto-fraud-discovery | Insurance fraud research |

## Communication Protocol
- Send: write .md to ../TARGET_BOT/inbox/from-SENDER-YYYY-MM-DD-subject.md
- Receive: check inbox/, act, move to inbox/processed/
- Commit: git add -A && git commit -m "BOT_NAME: description" && git push
