# Quick Reference Card - GitHub Agentic Workflows Workshop

## One-Page Cheat Sheet

---

## 🚀 SETUP COMMANDS

```bash
# Install CLI (Windows)
winget install --id GitHub.cli

# Install CLI (Mac)
brew install gh

# Install extensions
gh extension install github/gh-aw
gh extension install github/gh-copilot

# Authenticate
gh auth login

# Store Copilot token
gh aw secrets set COPILOT_GITHUB_TOKEN --value "YOUR_TOKEN"

# Verify secrets are configured
gh aw secrets bootstrap
```

---

## 📝 THREE CREATION METHODS

### 1. Interactive CLI (Simple)

```bash
gh aw create
# Follow prompts
```

### 2. Cloud Agent (Better)

```bash
# Go to your repository on GitHub.com
# Click the Agent tab
# Use the agent to create workflows
# Paste: "Create a workflow for GitHub Agentic Workflows
# using https://raw.githubusercontent.com/github/gh-aw/main/create.md
# The purpose is to [YOUR DESCRIPTION]"
```

### 3. Repository Agent (Best)

```bash
gh aw init
git add .github/aw/ && git commit -m "Init" && git push
# Open VS Code Copilot Chat, type /agents
# Select agentic-workflows agent from the UI
```

---

## 🎯 COMMON WORKFLOW PATTERNS

### Daily Status

```
Run daily at 9 AM and create an issue summarizing:
- Commits from yesterday
- PRs needing review
- Issues created/closed
- CI/CD failures
Title: "Daily Standup - [date]"
```

### CI Coach

```
When PR opened, analyze changes for potential issues:
- Missing tests
- Breaking changes
- Common mistakes
Comment with proactive suggestions.
```

### Continuous Tests

```
Run daily, find 3 files with inadequate tests.
Generate unit tests following repo conventions.
Create PR with new tests. Work with C#, JS, Python.
```

### Issue Triage

```
When issue opened, analyze and:
- Determine type (bug/feature/question)
- Add labels
- Estimate complexity
- Check for duplicates
- Post welcoming comment
```

### Repository Assistant

```
Run daily, review all issues:
- Close old automation issues
- Categorize issues
- Identify stale items
- Create "Health Dashboard" summary
```

---

## 🔧 ESSENTIAL GIT COMMANDS

```bash
# Clone and setup
git clone https://github.com/microsoft/CopilotAdventures.git
cd CopilotAdventures
git remote remove origin
git remote add origin https://github.com/YOU/YOUR-REPO.git
git push -u origin main

# Commit workflow
git add .github/workflows/WORKFLOW-NAME.yml
git commit -m "Add workflow: DESCRIPTION"
git push
```

---

## 🎮 WORKFLOW MANAGEMENT

```bash
# List workflows
gh workflow list

# View runs
gh run list

# Watch specific run
gh run watch

# Manually trigger
# (Go to Actions tab → Select workflow → Run workflow)

# Verify secrets are configured
gh aw secrets bootstrap
```

---

## ⚠️ TROUBLESHOOTING

**`gh aw` not found:**

```bash
gh extension install github/gh-aw
```

**Workflow not triggering:**

- Settings → Actions → General
- ✅ Allow all actions
- ✅ Read and write permissions
- ✅ Allow GitHub Actions to create PRs

**Authentication issues:**

```bash
gh auth refresh
```

**Token errors:**

- Regenerate PAT with "Copilot" permission
- Settings → Developer settings → Personal access tokens

---

## 📚 QUICK LINKS

- **Docs:** https://github.github.com/gh-aw/
- **Quick Start:** https://github.github.com/gh-aw/setup/quick-start/
- **Peli's Factory:** https://github.github.com/gh-aw/blog/2026-01-12-welcome-to-pelis-agent-factory/
- **Community:** https://github.com/orgs/community/discussions/186451
- **Workflows:** https://github.com/githubnext/agentics
- **Discord:** https://gh.io/next-discord

---

## ✅ REPOSITORY SETUP CHECKLIST

- [ ] Create repository on GitHub
- [ ] Enable Issues & Discussions
- [ ] Set Actions permissions (read/write)
- [ ] Allow Actions to create PRs
- [ ] Clone CopilotAdventures
- [ ] Push to your repository
- [ ] Create fine-grained PAT with Copilot access
- [ ] Store token: `gh aw secrets set COPILOT_GITHUB_TOKEN`
- [ ] Run `gh aw init` (after first workflow)

---

## 🎓 EXERCISES ORDER

1. ☑️ Daily standup status (interactive CLI)
2. ☑️ CI Coach (cloud agent)
3. ☑️ CI Doctor (cloud agent)
4. ☑️ Continuous test updates (cloud agent)
5. ☑️ Initialize repository (`gh aw init`)
6. ☑️ AGENTS.md maintenance (repo agent)
7. ☑️ Repository assistant (repo agent)
8. ☑️ Issue triage (repo agent)
9. ☑️ Create Ruby issue & `/plan`
10. ☑️ Reuse workflows (`gh aw add githubnext/agentics/...`)
11. ☑️ Workflow maintenance automation

---

## 🛡️ SAFETY REMINDERS

- ✅ Review all AI-generated PRs before merging
- ✅ Start with read-only workflows
- ✅ Use safe-outputs for writes
- ✅ Set GitHub Actions spending limits
- ✅ Never commit tokens or secrets
- ✅ Test on private repos first

---

## 💡 PRO TIPS

- **Be specific** in workflow descriptions
- **Reference docs** with URLs in prompts
- **Start simple**, add complexity gradually
- **Use checkpoints** to ensure workflows work
- **Iterate** - refine prompts based on results
- **Share** successful workflows with community

---

**GitHub Copilot Dev Days 2026**  
**Workshop:** From Code to Automation  
**Resources:** [Your repo link]

**Keep this card handy! 📌**

---

### Notes Space

Use this space for your own notes during the workshop:

```









```

---

**Print this page for quick reference during the workshop!**
