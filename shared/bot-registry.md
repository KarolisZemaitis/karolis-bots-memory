# Bot Registry

## Active Bots

| Bot Name | Directory | Purpose | Telegram |
|----------|-----------|---------|----------|
| Chief of Staff | /chief-of-staff-bot | Fleet coordinator, strategic advisor | @karolis_chief_of_staff1_bot |
| Briefing Bot | /briefing-bot | Daily morning briefings, monitoring | @karolis_briefing1_bot |
| Assistant Bot | /assistant-bot | Daily tasks, knowledge help | @karolis_assistant1_bot |
| Insurance Detector | /auto-fraud-discovery | Auto insurance fraud research | @karolis_insurance_detector1_bot |

## Communication Protocol

### Sending Messages
1. Write a .md file to ../TARGET_BOT/inbox/
2. Filename: from-SENDER-YYYY-MM-DD-subject.md
3. Include: what you need, why, urgency, expected response

### Receiving Messages
1. Check inbox/ for new .md files
2. Read and act on them
3. Move processed messages to inbox/processed/

### After Any File Changes
git add -A && git commit -m "BOT_NAME: description" && git push

## Adding New Bots
1. Create a new directory in this repo with CLAUDE.md, memory.md, inbox/, inbox/processed/
2. Update this registry
3. Create Telegram bot via @BotFather (/newbot)
4. Create config directory: mkdir -p ~/.claude-NEWBOTNAME/
5. Copy config: cp -r ~/.claude/settings* ~/.claude-NEWBOTNAME/ && cp -r ~/.claude/plugins* ~/.claude-NEWBOTNAME/
6. Add to ~/.claude/start-bots.sh (add kill line + new-session line)
7. Run startbots
8. Pair: tmux attach -t BOTNAME > message bot in Telegram > /telegram:access pair CODE > /telegram:access policy allowlist > Ctrl+B then D
