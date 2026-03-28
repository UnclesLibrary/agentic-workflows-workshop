# GitHub Agentic Workflows Workshop - Participant Handout

## Quick Reference Guide

**Workshop:** From Code to Automation: Mastering GitHub Agentic Workflows  
**Duration:** 2 hours  
**Date:** [Your Event Date]

---

## 📋 Prerequisites

Before starting, ensure you have:

- [ ] GitHub account (sign up at github.com)
- [ ] GitHub Copilot access (start trial at github.com/copilot)
- [ ] Laptop with admin rights to install software
- [ ] Internet connection

---

## 🛠️ Setup Commands

### 1. Install GitHub CLI

**Windows:**

```powershell
winget install --id GitHub.cli
```

**Mac:**

```bash
brew install gh
```

**Linux (Debian/Ubuntu):**

```bash
# Install from GitHub CLI repository
sudo mkdir -p -m 755 /etc/apt/keyrings
wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh -y

# For other distributions (Fedora, Arch, etc.):
# See: https://github.com/cli/cli/blob/trunk/docs/install_linux.md
```

**Verify:**

```bash
gh --version
# Should show version 2.87.3 or higher
```

### 2. Install Extensions

```bash
# Install gh-copilot (optional but recommended)
gh extension install github/gh-copilot

# Install gh-aw (required)
gh extension install github/gh-aw

# Verify installation
gh aw --version
# Should show version 0.51.5 or higher
```

### 3. Authenticate with GitHub

```bash
gh auth login

# Follow the prompts:
# ? Where do you use GitHub? → GitHub.com
# ? What is your preferred protocol for Git operations? → HTTPS
# ? Authenticate Git with your GitHub credentials? → Yes
# ? How would you like to authenticate GitHub CLI? → Login with a web browser

# Copy the one-time code (e.g., XXXX-XXXX)
# Press Enter to open https://github.com/login/device in your browser
# Paste the code in the browser and authorize

# Expected output:
# ✓ Authentication complete.
# ✓ Logged in as <your-github-username>
```

---

## 🎯 Repository Setup

### 1. Create Your Repository on GitHub

**Note:** If you're not signed in to github.com in your web browser, sign in first.

1. Go to github.com → Click **New** (top left, next to "Top Repositories")
   
   ![New repository button](images/new-repository.png)

2. **Choose owner:** Select your GitHub user account
3. **Name:** `copilot-adventures-[yourname]`
4. **Visibility:** Public or Private (your choice)
5. **Do NOT** add README, .gitignore, or license
6. Click "Create repository"

### 2. Configure Repository Settings

**Actions Permissions:**

- Settings → Actions → General
- ✅ Allow all actions and reusable workflows
- Workflow permissions: ✅ Read and write permissions
- ✅ Allow GitHub Actions to create and approve pull requests
- **Click "Save"** to apply changes

**Enable Features:**

- Settings → General → Features
- ✅ Issues
- ✅ Discussions
- **Note:** Feature changes are applied immediately (no save button needed)

### 3. Clone and Push CopilotAdventures

```bash
# Clone Microsoft's CopilotAdventures
git clone https://github.com/microsoft/CopilotAdventures.git
cd CopilotAdventures

# Remove original remote
git remote remove origin

# Add YOUR repository as remote (replace with your username/repo)
git remote add origin https://github.com/YOUR-USERNAME/copilot-adventures-YOURNAME.git

# Push to your repository
git push -u origin main
```

### 4. Create PAT (Personal Access Token)

1. Click on your **profile icon** (top-right) → **Settings** → **Developer settings** (bottom left of the new page)
2. **Personal access tokens** → **Fine-grained tokens**
3. Click "**Generate new token**"
4. **Token name:** `Agentic Workflows Copilot Token`
5. Leave the defaults:
   - **Resource owner:** Your GitHub user account
   - **Expiration:** 30 days
   - **Repository access:** Public Repositories (only)
6. **Permissions:** Scroll down and click "**Add permission**" → Select **"Copilot Requests"**
   - This allows the user of this token to make Copilot requests on your behalf, using your premium requests and calls
   
   ![Generate token screenshot](images/generate-token.png)

7. Click "**Generate token**" → **Copy it immediately** (you won't see it again)!

```bash
# Store token (paste your actual token)
gh aw secrets set COPILOT_GITHUB_TOKEN --value "YOUR_TOKEN_HERE"

# Verify required secrets are configured
gh aw secrets bootstrap
```

---

## 📝 Workshop Exercises

### Introduction: Why Agentic Workflows?

**The Challenge:**

Imagine a team of 9 people working on a repository. Everyone is busy with their tasks, and while you generally know what your team is working on, you're never fully in touch with everything that's been completed or what's coming next. You've added daily standups and progress boards, but challenges remain:

- What happens when people have a day off?
- What if someone forgets to mention critical progress during standup?
- Who notices that PR sitting open for 2 days without a review?
- How do you track the actual state of the repository between standups?

**The Solution:**

Instead of relying solely on humans to track and communicate everything, we'll create automated assistants that work continuously in the background. These agentic workflows will:

- Generate daily summaries of real repository activity
- Monitor PRs and issues that need attention
- Provide objective data for standups and planning
- Work 24/7 without taking days off
- Never forget to check or report on important changes

**What We're Building:**

Throughout these exercises, you'll progressively build an ecosystem of intelligent automations that transform your repository into a self-organizing, self-reporting system. Each workflow adds a new capability, and together they create comprehensive visibility into your project's health and progress.

**How We're Building:**

You'll experience three different approaches to creating workflows, each with increasing quality and sophistication:

1. **Interactive CLI** (`gh aw new`) - Quick and interactive, good for learning
2. **Cloud Agent** (web browser agent tab) - Better quality by referencing documentation
3. **Repository Agent** (VS Code Copilot Chat after `gh aw init`) - Best quality with repository context

Let's start with the most fundamental need: knowing what happened in your repository each day.

---

### Exercise 1: Daily Standup Status

**Goal:** Create a workflow that generates a daily summary of repository activity to support your standup meetings.

**Method:** We'll use the interactive CLI (`gh aw new`) to learn the fundamentals of workflow creation.

**Step 1: Create the workflow**

```bash
gh aw new
```

You'll be guided through several prompts:

**1. What should we call this workflow?**
```
daily-report
```

**2. When should this workflow run?**
- Choose: `Schedule (daily, scattered execution time)`

**3. Which AI engine should process this workflow?**
- Choose: `copilot - GitHub Copilot CLI`

**4. Which tools should the AI have access to?**
- Select:
  - `github` - GitHub API tools (issues, PRs, comments, repos)
- Tools enabled:
  - `create-issue` - Create a new GitHub issue
  - `add-comment` - Add a comment to an issue, PR, or discussion
  - `close-issue` - Close a GitHub issue
  - `update-issue` - Update an existing GitHub issue

**5. Network Access Control**
- Leave defaults (no external network access needed)

**6. What should this workflow do?** (Description)
```
Run daily at 9 AM and create an issue with a summary of repository activity from past 24 hours. Include commits, pull requests, issues, and CI/CD failures.
```

**Step 2: Review the generated files**

The command creates **two files** in `.github/workflows/`:

1. **`daily-report.md`** - The editable source workflow
2. **`daily-report.lock.yml`** - The compiled GitHub Actions workflow

**Understanding the files:**

**`daily-report.md`** contains:
- **Frontmatter** (YAML between `---` markers): Configuration defining triggers, permissions, and tools
- **Natural language instructions**: Your description in markdown format

**`daily-report.lock.yml`** is the compiled workflow that:
- Contains a simplified version of your prompt
- Is what GitHub Actions actually executes
- Gets regenerated when you change the `.md` file

📚 **Learn more:** [How Agentic Workflows Work](https://github.github.com/gh-aw/introduction/how-they-work/)

**Step 3: Observe the limitation**

Open `.github/workflows/daily-report.lock.yml` and look at the prompt. It's very basic - just your description. This works, but we can achieve much better results.

**Why this matters:** The quality of the AI's output depends heavily on the quality and detail of the instructions. The simple interactive CLI creates a minimal prompt, which means the workflow might:
- Miss important details
- Not format output consistently
- Lack error handling
- Be less reliable

**What's next:** In the following exercises, we'll use more sophisticated approaches that generate better prompts and higher-quality workflows.

**Step 4: Commit and test**

```bash
# Review the generated files
cat .github/workflows/daily-report.md
cat .github/workflows/daily-report.lock.yml

# Commit both files
git add .github/workflows/daily-report.md .github/workflows/daily-report.lock.yml
git commit -m "Add daily report workflow (basic version)"
git push
```

**Step 5: Manually trigger to test**

Since it's scheduled for daily execution, trigger it manually to see it work:

1. Go to your repository on GitHub
2. Click **Actions** tab
3. Select **daily-report** workflow
4. Click **Run workflow** button
5. Watch it execute and create an issue

---

### Exercise 2: CI Coach

**Why: Building the Backbone of Your DevOps Practice**

Now that you have visibility into daily activity, let's focus on the backbone of your validation system: your **Continuous Integration (CI) pipeline**.

Your CI pipeline is critical because it:
- **Triggers on each change** - Every commit, every PR gets validated
- **Validates each update** - Runs tests, checks code quality, enforces standards
- **Deploys to customers** - When successful, it puts your work in users' hands

As a team improving your DevOps practices, you need guardrails before letting AI run fully agentic. A healthy CI pipeline is non-negotiable because you want it to be:
- **Quick enough** - Fast feedback means you can wait for results and fix issues immediately
- **Consistent enough** - It's your single source of truth for "is this ready?"
- **Complete enough** - Tests all scenarios so you ship with confidence

**The challenge:** Teams often set up CI once and then the codebase evolves without the pipeline keeping pace. New dependencies get added, test patterns change, edge cases emerge - but the CI configuration stays static. You need constant validation that your pipeline is keeping up with your code.

**What: A CI Coach That Has Your Back**

The CI Coach workflow provides:
- **Proactive guidance** - Catches issues before CI runs, saving time
- **Evolutionary awareness** - Notices when your codebase has evolved beyond your current CI setup
- **Continuous nudges** - Suggests improvements as patterns emerge
- **Early warnings** - Spots potential failures before they happen

Instead of waiting for CI to fail and then reacting, you get coaching on every PR that helps you maintain a world-class pipeline.

**How: Create Your CI Coach**

**Method:** We'll use the cloud agent (web browser) which produces better quality workflows by referencing documentation.

**Step 1: Create the workflow using the cloud agent**

1. Go to your repository on GitHub.com in your web browser
2. Click on the **Agent** tab
3. Provide this prompt to the agent:

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose of the workflow is to act as a CI Coach that runs when a pull request is opened or updated. It should:
1. Analyze the code changes for potential CI/CD issues
2. Check if tests are likely to pass
3. Look for common mistakes (missing dependencies, syntax issues, breaking changes)
4. Comment on the PR with proactive suggestions before CI runs
5. Be encouraging and helpful in tone

Use the pull_request trigger and comment on PRs using safe-outputs.
```

**Step 2: Review and merge the generated PR**

The cloud agent creates a **Pull Request** with the workflow files. 

1. Go to your repository on GitHub → **Pull Requests** tab
2. Review the PR created by the agent (titled something like "Add CI Coach workflow")
3. Verify the workflow files look correct:
   - `.github/workflows/ci-coach.md` (source workflow)
   - `.github/workflows/ci-coach.lock.yml` (compiled workflow)
4. **Merge the PR to main**

**Step 3: Manually trigger the CI Coach**

Since the CI Coach triggers on pull requests, let's test it manually first:

1. Go to your repository → **Actions** tab
2. Select **ci-coach** workflow (or similar name)
3. Click **Run workflow** button → Run workflow
4. Watch it execute

**Step 4: Check the outcome**

After the workflow completes, check your repository:

**Question to consider:** Did you receive a:
- 📝 **Pull Request** with suggested changes?
- 💬 **Discussion** post with recommendations?
- 🎯 **Issue** with analysis and suggestions?

**Important:** You can configure how the CI Coach communicates with you! The workflow can be set to create PRs for actionable changes, issues for recommendations, or discussions for general feedback. 

Which format do you prefer for receiving CI coaching feedback? Think about:
- PRs = Immediate actionable changes ready to review
- Issues = Trackable recommendations you can prioritize
- Discussions = Conversational feedback for team consideration

**Key Insight:** The CI Coach doesn't just check syntax—it analyzes your repository's testing infrastructure and identifies opportunities for improvement. It recognizes when your codebase has evolved beyond your current CI setup and provides specific, measurable recommendations to keep your pipeline aligned with your code.

This continuous feedback strengthens your guardrails as you prepare for more autonomous workflows.

---

### Exercise 3: CI Doctor

**Access the cloud agent:**

1. Go to your repository on GitHub.com in your web browser
2. Click on the **Agent** tab
3. Use the agent to create the workflow

**Prompt:**

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose of the workflow is to act as a CI Doctor that runs when a workflow_run fails. It should:
1. Analyze the failure logs
2. Identify the root cause
3. Search for similar issues in the repository history
4. Create a detailed issue with:
   - Failure summary
   - Root cause analysis
   - Suggested fixes
   - Links to relevant documentation
5. If the fix is simple (dependency update, typo), attempt to create a PR

Use the workflow_run trigger with completed status and failure conclusion.
```

**Save the generated workflow to:** `.github/workflows/ci-doctor.md` and `.github/workflows/ci-doctor.lock.yml`

```bash
git add .github/workflows/ci-doctor.md .github/workflows/ci-doctor.lock.yml
git commit -m "Add CI Doctor workflow"
git push
```

---

### Exercise 4: Continuous Test Updates

**Access the cloud agent:**

1. Go to your repository on GitHub.com in your web browser
2. Click on the **Agent** tab
3. Use the agent to create the workflow

**Prompt:**

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose of the workflow is to continuously improve test coverage. It should run daily and:
1. Analyze the codebase to find 3 files with missing or inadequate tests
2. Generate meaningful unit tests for those files
3. Ensure tests follow the existing test conventions in the repository
4. Create a pull request with the new tests
5. Limit to 3 test additions per day to keep PRs manageable

The workflow should work across C#, JavaScript, and Python files in the Solutions/ directory.

Use a daily schedule trigger and create PRs with safe-outputs.
```

**Save the generated workflow to:** `.github/workflows/continuous-test-updates.md` and `.github/workflows/continuous-test-updates.lock.yml`

```bash
git add .github/workflows/continuous-test-updates.md .github/workflows/continuous-test-updates.lock.yml
git commit -m "Add continuous test updater"
git push
```

---

### Exercise 5: Initialize Repository

```bash
# Initialize agentic workflows in your repository
gh aw init

# This creates .github/aw/ directory with configuration
# Commit the changes
git add .github/aw/
git commit -m "Initialize GitHub Agentic Workflows"
git push
```

**Now use VS Code Copilot Chat with repository agent:**

1. Open VS Code Copilot Chat
2. Type `/agents` to view available agents
3. Select the agentic-workflows agent from the UI
4. Use this prompt:

```
create a workflow that keeps the AGENTS.md file up to date.

It should run weekly, review merged pull requests and updated source files since the last run, then open a pull request that keeps AGENTS.md accurate and current.
```

**Save and commit the generated workflow.**

---

### Exercise 6: Repository Assistant

**Use VS Code Copilot Chat with repository agent:**

1. Type `/agents` and select agentic-workflows agent
2. Use this prompt:

```
I'm noticing that my issues are growing overwhelming with all these workflow-generated issues. Create a repository assistant workflow that:

1. Runs daily
2. Reviews all open issues
3. Categorizes them (bugs, features, maintenance, automation-generated)
4. Closes stale automation issues (like old daily standups)
5. Prioritizes issues that need human attention
6. Creates a summary issue: "Repository Health Dashboard"
7. Suggests which issues should be moved to Discussions

The assistant should be helpful and respect issues created by humans vs automation.
```

**Save and commit:** `.github/workflows/repository-assistant.yml`

---

### Exercise 7: Issue Triage

**Use VS Code Copilot Chat with repository agent:**

1. Type `/agents` and select agentic-workflows agent
2. Use this prompt:

```
create an issue triage workflow that runs when issues are opened. It should:

1. Analyze the issue content
2. Determine if it's a bug, feature request, question, or enhancement
3. Add appropriate labels
4. Estimate complexity (simple, moderate, complex)
5. Check if it's a duplicate of existing issues
6. If it's a question, suggest moving to Discussions
7. If it's well-defined, add "ready-for-development" label
8. Add a welcoming comment with the analysis

Be friendly and helpful in tone.
```

**Save and commit:** `.github/workflows/issue-triage.yml`

---

### Exercise 8: Feature Planning with /plan

1. **Create a new issue in GitHub:**
   - Title: `Add Ruby support to CopilotAdventures`
   - Description:

     ```
     Currently we have Python, C#, and JavaScript solutions. Add Ruby adventure
     solutions following the same guidelines and structure as the other languages.

     Requirements:
     - Create Ruby solutions for at least 3 beginner adventures
     - Follow the existing naming conventions
     - Add README for Ruby setup instructions
     - Ensure solutions produce the same output as other languages
     ```

2. **Wait for issue triage to analyze it (automatic)**

3. **Comment on the issue:**

   ```
   /plan
   ```

4. **Watch the planning workflow break down the feature into tasks**

---

### Exercise 9: Implementation Workflow

**Use VS Code Copilot Chat with repository agent:**

1. Type `/agents` and select agentic-workflows agent
2. Use this prompt:

```
create a workflow that triggers when someone comments "/implement" on an issue. The workflow should:

1. Read the issue description and any plans
2. Create a new branch for the feature
3. Implement the first task in the plan
4. Run tests to verify it works
5. Create a draft pull request
6. Comment back on the original issue with progress

This enables iterative development triggered by humans.
```

**Then test it:**

- Comment `/implement` on the Ruby issue
- Watch the workflow create a branch and start implementation

---

### Exercise 10: Reuse Workflows

```bash
# Add a workflow from the community library
gh aw add githubnext/agentics/continuous-documentation-updates

# Review what was added
cat .github/workflows/continuous-documentation-updates.yml

# Commit
git add .github/workflows/continuous-documentation-updates.yml
git commit -m "Add continuous documentation updates"
git push
```

---

### Exercise 11: Workflow Maintenance

**Use VS Code Copilot Chat with repository agent:**

1. Type `/agents` and select agentic-workflows agent
2. Use this prompt:

```
create a workflow called "agentics-maintenance" that:

1. Runs weekly
2. Checks if any workflows in our repository were imported from githubnext/agentics
3. Compares our versions to the latest versions in the remote repository
4. If updates are available:
   - Creates a branch
   - Updates the workflows
   - Runs tests to ensure compatibility
   - Creates a PR with changelog of what changed
5. Labels PR as "dependencies" and "workflows"

This keeps our imported workflows up to date automatically.
```

**Save and commit:** `.github/workflows/agentics-maintenance.yml`

---

## 🎯 Useful Commands

### View Workflows

```bash
# List all workflows
gh workflow list

# View workflow runs
gh run list

# View specific run
gh run view <run-id>

# Watch a running workflow
gh run watch
```

### Manage Secrets

```bash
# Verify required secrets are configured
gh aw secrets bootstrap

# Set a secret
gh aw secrets set SECRET_NAME --value "secret-value"
```

### Workflow Management

```bash
# Validate workflows
gh aw validate

# Update gh-aw extension
gh extension upgrade gh-aw

# View gh-aw help
gh aw --help
```

---

## 🔥 Troubleshooting

### Common Issues

**`gh aw` command not found**

```bash
gh extension install github/gh-aw
gh extension list  # Verify installation
```

**Workflow not triggering**

- Check Settings → Actions → Permissions
- Ensure read/write permissions enabled
- Verify workflow YAML is valid

**COPILOT_GITHUB_TOKEN errors**

- Regenerate token with proper permissions
- Ensure token has "Copilot" scope
- Check token hasn't expired

**PR not created by workflow**

- Settings → Actions → Workflow permissions
- Enable "Allow GitHub Actions to create and approve pull requests"

**Authentication fails**

```bash
gh auth refresh
# Or logout and login again
gh auth logout
gh auth login
```

---

## 📚 Resources

### Documentation

- **GitHub Agentic Workflows:** https://github.github.com/gh-aw/
- **Quick Start Guide:** https://github.github.com/gh-aw/setup/quick-start/
- **How It Works:** https://github.github.com/gh-aw/introduction/how-they-work/
- **Security Architecture:** https://github.github.com/gh-aw/introduction/architecture/

### Community

- **Peli's Agent Factory:** https://github.github.com/gh-aw/blog/2026-01-12-welcome-to-pelis-agent-factory/
- **Community Discussions:** https://github.com/orgs/community/discussions/186451
- **GitHub Next Discord:** https://gh.io/next-discord
- **Workflow Library:** https://github.com/githubnext/agentics

### CopilotAdventures

- **Main Repository:** https://github.com/microsoft/CopilotAdventures
- **Adventures:** Educational coding challenges in multiple languages
- **Contribute:** Follow CONTRIBUTING.md guidelines

---

## 💡 Tips & Best Practices

### Security

- ✅ Start with read-only workflows
- ✅ Use safe-outputs for all writes
- ✅ Review all AI-generated PRs before merging
- ✅ Set spending limits on GitHub Actions
- ✅ Never commit tokens or secrets
- ✅ Use fine-grained PATs with minimal permissions

### Workflow Design

- ✅ Start simple, add complexity gradually
- ✅ Be descriptive in workflow prompts
- ✅ Reference documentation URLs for better results
- ✅ Test workflows on private repos first
- ✅ Use meaningful workflow names
- ✅ Add comments explaining workflow purpose

### Maintenance

- ✅ Monitor workflow runs regularly
- ✅ Update workflows when patterns improve
- ✅ Archive workflows you're not using
- ✅ Keep documentation in sync with workflows
- ✅ Version control all changes
- ✅ Use workflow maintenance automation

---

## 🎓 What You've Learned

By completing this workshop, you now know how to:

- [x] Install and configure GitHub Agentic Workflows
- [x] Create workflows using three different methods (CLI, Cloud, Repository Agent)
- [x] Implement continuous improvement patterns
- [x] Automate issue management and triage
- [x] Use `/plan` for feature breakdown
- [x] Trigger workflows from comments
- [x] Reuse workflows from other repositories
- [x] Maintain workflows automatically
- [x] Apply security guardrails
- [x] Build self-organizing repository systems

---

## 🚀 Next Steps

### Immediate (This Week)

- Experiment with your CopilotAdventures repository
- Add one workflow to a personal project
- Join the GitHub Next Discord community
- Share your workflows in GitHub Discussions

### Short Term (This Month)

- Propose agentic workflows to your team
- Build a workflow library for your organization
- Contribute workflows to githubnext/agentics
- Help others in the community

### Long Term (This Year)

- Implement comprehensive automation in team repos
- Present learnings to your organization
- Mentor others on agentic workflows
- Build advanced multi-step automation systems

---

## 📞 Stay Connected

**Workshop Resources:**

- Workshop repository: [Add your repo link]
- Facilitator contact: [Add your email/GitHub]
- Event page: [Add Copilot Dev Days link]

**Feedback:**

- Workshop survey: [Add survey link]
- GitHub Discussions: [Add discussion link]
- Twitter/X: #GitHubCopilotDevDays

---

**Event:** GitHub Copilot Dev Days 2026  
**Workshop:** From Code to Automation: Mastering GitHub Agentic Workflows  
**Date:** [Your Event Date]  
**Location:** [Your Location]

**Thank you for participating! 🎉**

Keep automating, keep improving, and remember: humans provide direction, AI handles execution.

---

_This handout is available at: [Add link to this file in your repository]_
