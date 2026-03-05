# Facilitator Guide: GitHub Agentic Workflows Workshop

## "From Code to Automation: Mastering GitHub Agentic Workflows"

**Total Duration:** 2 hours  
**Format:** Hands-on workshop with live coding  
**Difficulty:** Beginner to Intermediate

---

## Pre-Workshop Checklist (30 minutes before)

- [ ] Test WiFi connectivity and bandwidth
- [ ] Verify projector/screen connection
- [ ] Open all necessary tabs/windows:
  - GitHub (logged in)
  - VS Code
  - Terminal with gh CLI
  - Workshop repository
  - Documentation: https://github.github.com/gh-aw/
- [ ] Test `gh aw` CLI is working
- [ ] Have backup examples ready
- [ ] Print participant handouts (optional)
- [ ] Create workshop issue on your demo repo
- [ ] Have emergency PAT token ready
- [ ] Test live demo workflows

---

## Workshop Timeline

| Time | Section                       | Duration | Activity                       |
| ---- | ----------------------------- | -------- | ------------------------------ |
| 0:00 | Intro & Welcome               | 15 min   | Presentation                   |
| 0:15 | Setup                         | 15 min   | Installation & Config          |
| 0:30 | Exercise 1: Daily Status      | 10 min   | First workflow with wizard     |
| 0:40 | Exercise 2: CI Coach & Doctor | 15 min   | Using cloud agent              |
| 0:55 | Exercise 3: Test Automation   | 10 min   | Scheduled workflows            |
| 1:05 | Exercise 4: Repository Init   | 10 min   | `gh aw init` and agents        |
| 1:15 | Exercise 5: Issue Management  | 15 min   | Growing complexity pattern     |
| 1:30 | Exercise 6: Planning & Triage | 15 min   | `/plan` and reuse workflows    |
| 1:45 | Exercise 7: Advanced Patterns | 15 min   | Remote workflows & maintenance |
| 2:00 | Wrap-up & Q&A                 | 15 min   | Retrospective                  |

---

## Section 0: Introduction & Welcome (0:00-0:15) [15 min]

### Opening (2 min)

**Say:**

> "Welcome to our GitHub Agentic Workflows workshop! By the end of today, you'll have a repository with intelligent automations running that improve your code, manage your issues, and support your daily development rituals—all written in natural language. No complex YAML required."

**Key Points:**

- This is hands-on—you'll be coding along
- Progressive complexity—we start simple
- You'll leave with a working repository you can continue using
- Questions are welcome anytime

### Why GitHub Agentic Workflows? (5 min)

**SLIDE 1: The Problem**

- Development teams struggle with repetitive tasks
- DevOps practices are powerful but complex
- GitHub Actions requires YAML expertise
- CI/CD failures interrupt flow
- Documentation drifts out of sync
- Issue triage becomes overwhelming

**SLIDE 2: The Solution**

- GitHub Agentic Workflows = Automation + AI
- Write workflows in natural language (markdown)
- AI agents execute on GitHub Actions
- Continuous improvement on autopilot
- Support daily rituals (standups, planning, reviews)

**DEMO:** Show a workflow file side-by-side with what it does

```markdown
# Daily Status for Standup

Run daily at 9 AM and post a summary of repository activity in a new issue.

Include:

- Commits since yesterday
- Open pull requests needing review
- Issues created or closed
- Failed CI/CD runs

Title: "Daily Standup Summary - [date]"
```

**Say:**

> "That's it. That's the entire workflow. The AI figures out how to query the GitHub API, format the data, create the issue. You describe what you want, AI makes it happen."

### Key Concepts (5 min)

**SLIDE 3: Three Ways to Create Workflows**

1. **CLI Wizard** (`gh aw create`)
   - Guided prompts
   - Quick and simple
   - Good for learning
   - Basic template substitution

2. **Cloud Agent** (prompt with URL)
   - Use before `gh aw init`
   - References documentation automatically
   - Higher quality results
   - Better for complex workflows

3. **Repository Agent** (VS Code/Chat after `gh aw init`)
   - Best quality results
   - Context-aware
   - Can reference existing workflows
   - Integrates with Copilot

**SLIDE 4: Guardrails & Safety**

- Workflows run in sandboxed GitHub Actions
- Read-only by default
- Writes only through `safe-outputs`
- Human approval gates available
- SHA-pinned dependencies
- Network isolation options

**Say:**

> "Safety first. These are AI agents with access to your repository. By default, they can only read. Any write operations go through sanitized safe-outputs. You control what they can do."

**SLIDE 5: What We'll Build Today**

Show visual progression:

```
Simple → Progressive → Sophisticated

1. Daily status report
2. CI coach & doctor
3. Automated test updates
4. Issue assistant & triage
5. Planning automation
6. Documentation maintenance
7. Workflow reuse & remote updates
```

### Transition to Setup (1 min)

**Say:**

> "Alright, let's get hands-on. First, we need to set up our environment. This will take about 15 minutes, but it's worth getting right. Follow along step-by-step."

---

## Section 1: Setup (0:15-0:30) [15 min]

### Installation Phase (5 min)

**Screen Share:** Terminal window

**Talk through each command:**

```bash
# 1. Install GitHub CLI (if not already installed)
# Windows (using winget)
winget install --id GitHub.cli

# Mac
brew install gh

# Verify installation
gh --version
```

```bash
# 2. Install gh copilot extension (optional but recommended for later)
gh extension install github/gh-copilot

# 3. Install gh-aw extension
gh extension install github/gh-aw

# Verify
gh aw --version
```

**Checkpoint:** "Raise your hand if you see a version number for `gh aw`"

### Authentication (3 min)

```bash
# Authenticate with GitHub
gh auth login

# Follow prompts:
# - GitHub.com
# - HTTPS
# - Yes (authenticate with web browser)
# - Copy one-time code
# - Opens browser → Paste code → Authorize
```

**Common Issue:** Browser doesn't open

- Manually go to github.com/login/device
- Enter code shown in terminal

**Checkpoint:** "Everyone should see 'Logged in as [username]'"

### Repository Setup (7 min)

**Step 1: Create new repository**

**Say:** "We'll each create our own repository so you can continue using it after the workshop."

**Screen Share:** GitHub web UI

1. Go to github.com → New repository
2. Name: `copilot-adventures-[yourname]`
3. **Important:** Public or Private (your choice)
4. **Do NOT** add README, .gitignore, or license
5. Click "Create repository"

**Step 2: Configure repository settings**

Navigate to Settings:

**Actions Permissions:**

- Settings → Actions → General
- ✅ Allow all actions and reusable workflows
- Workflow permissions: ✅ Read and write permissions
- ✅ Allow GitHub Actions to create and approve pull requests

**Enable Features:**

- Settings → General → Features
- ✅ Issues
- ✅ Discussions

**Say:** "These settings let our workflows do their magic. Without read/write permissions, they can't create issues or pull requests."

**Step 3: Clone CopilotAdventures and push to your repo**

```bash
# Clone the Microsoft CopilotAdventures repository
git clone https://github.com/microsoft/CopilotAdventures.git
cd CopilotAdventures

# Remove original remote
git remote remove origin

# Add your new repository as remote
git remote add origin https://github.com/YOUR-USERNAME/copilot-adventures-YOURNAME.git

# Push to your repository
git push -u origin main
```

**Checkpoint:** "Check GitHub—you should see all the CopilotAdventures files in your repository now."

**Step 4: Create Fine-Grained PAT (Personal Access Token)**

**Say:** "We need a token so workflows can use Copilot to generate content."

**Screen Share:** GitHub Settings

1. Settings (top-right profile) → Developer settings → Personal access tokens → Fine-grained tokens
2. Generate new token
3. Name: `Agentic Workflows Copilot Token`
4. Expiration: 90 days (or workshop duration)
5. Repository access: Select your `copilot-adventures-*` repository
6. Permissions:
   - **Copilot**: Read-only (request access if needed)
7. Generate token
8. **Copy token** (you won't see it again)

```bash
# Store token in repository secrets
gh aw secrets set COPILOT_GITHUB_TOKEN --value "YOUR_TOKEN_HERE"
```

**Security Note:**

> "Never share this token or commit it to your repository. It's stored securely in GitHub secrets."

**Checkpoint:** "Run `gh aw secrets list` - you should see COPILOT_GITHUB_TOKEN listed."

### Setup Complete (1 min)

**Say:**

> "Great! Setup is done. Now we have:
>
> - GitHub CLI with gh-aw extension ✓
> - Our own copy of CopilotAdventures ✓
> - Repository properly configured ✓
> - Copilot token stored ✓
>
> Time to build some workflows!"

---

## Section 2: Exercise 1 - Daily Status Report (0:30-0:40) [10 min]

### Learning Objectives

- Create first workflow using CLI wizard
- Understand basic workflow structure
- See workflow run and produce results

### Introduction (1 min)

**Say:**

> "Let's start with something immediately useful: a daily standup report. Every morning at 9 AM, our repository will create an issue summarizing what happened yesterday. Perfect for remote teams or async standups."

### Live Code-Along (6 min)

**Step 1: Create workflow using wizard**

```bash
gh aw create
```

**Prompts and Responses:**

```
? What would you like to name this workflow?
> daily-standup-status

? What should this workflow do?
> Run daily at 9 AM and create an issue with a summary of repository activity from the past 24 hours. Include commits, pull requests, issues, and any CI/CD failures. Title: "Daily Standup - [date]"

? When should this workflow run?
> schedule (daily at 9 AM)

? Does the workflow need any special permissions?
> Issues: write, Contents: read, Pull Requests: read

? Review and confirm? (y/n)
> y
```

**Say while waiting:**

> "The wizard is generating the workflow file. It's using a template and substituting our description."

**Step 2: Review generated workflow**

```bash
# Open the generated workflow file
code .github/workflows/daily-standup-status.yml
```

**Point out:**

- YAML structure (they don't need to write this)
- Schedule trigger: `cron: '0 9 * * *'`
- The `uses: github/agentic-workflows` action
- Their description in the workflow

**Step 3: Commit and push**

```bash
git add .github/workflows/daily-standup-status.yml
git commit -m "Add daily standup status workflow"
git push
```

**Step 4: Trigger manually for demo**

**Say:** "We don't want to wait until tomorrow at 9 AM. Let's trigger it manually."

**Screen Share:** GitHub Actions tab

1. Go to Actions tab in repository
2. Find "Daily Standup Status" workflow
3. Click "Run workflow" → Run workflow
4. Watch it run (takes 1-2 minutes)

### Review Results (3 min)

**Navigate to Issues tab**

**Point out:**

- New issue created by the workflow
- Structured summary: commits, PRs, issues
- Professional formatting
- Actionable information

**Say:**

> "This is now running every day at 9 AM automatically. You wake up, check your issues, and know exactly what happened yesterday. No manual work required."

**Discussion Questions:**

- "How would this help your team?"
- "What other daily summaries might be useful?"

**Checkpoint:** "Everyone should have a workflow running or completed. Raise your hand if you need help."

---

## Section 3: Exercise 2 - CI Coach & Doctor (0:40-0:55) [15 min]

### Learning Objectives

- Use cloud agent for better workflow quality
- Create workflows without initializing repository
- Understand reactive triggers (on failure)

### Introduction (2 min)

**Say:**

> "The wizard is great for simple workflows, but for more sophisticated ones, we want better quality. Let me introduce you to the **cloud agent approach**. This works BEFORE you run `gh aw init`, and it gives you much better results because it references the official documentation."

### CI Coach - Proactive Prevention (5 min)

**Say:**

> "CI Coach runs before your workflows to catch potential problems. Think of it as a pre-flight check."

**Step 1: Use cloud agent with documentation reference**

```bash
# Use @github/copilot with special prompt
gh copilot suggest
```

**Prompt:**

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

**Say while AI generates:**

> "Notice I'm giving the AI the URL to the creation guide. This means it can reference the exact patterns and best practices from the official docs. The quality is much better."

**Step 2: Save the generated workflow**

```bash
# Copy the output to a file
code .github/workflows/ci-coach.yml
# Paste the generated content
```

**Step 3: Commit and push**

```bash
git add .github/workflows/ci-coach.yml
git commit -m "Add CI Coach workflow"
git push
```

### CI Doctor - Reactive Healing (6 min)

**Say:**

> "CI Doctor is reactive—it runs AFTER a failure and tries to diagnose and fix the problem."

**Step 1: Create CI Doctor workflow**

```bash
gh copilot suggest
```

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

**Step 2: Save and push**

```bash
code .github/workflows/ci-doctor.yml
# Paste content
git add .github/workflows/ci-doctor.yml
git commit -m "Add CI Doctor workflow"
git push
```

**Step 3: Demonstrate the difference**

**Show side-by-side:**

- CLI wizard generated workflow (basic template)
- Cloud agent generated workflow (references docs, more sophisticated)

**Say:**

> "See the difference? The cloud agent version has better error handling, follows best practices from the docs, and is more comprehensive. Same prompt effort, better results."

### Review & Discussion (2 min)

**Key Takeaway:**

> "Use the wizard for learning and simple workflows. Use the cloud agent with documentation reference for production-quality workflows."

**Checkpoint:** "Everyone should have two new workflows: ci-coach and ci-doctor. Let's continue."

---

## Section 4: Exercise 3 - Continuous Test Updates (0:55-1:05) [10 min]

### Learning Objectives

- Create scheduled workflows
- Understand continuous improvement pattern
- See AI making incremental code changes

### Introduction (1 min)

**Say:**

> "Now let's tackle continuous improvement. Instead of one big push to add tests, why not add 3 tests every day automatically? Over time, your coverage improves without any manual effort."

### Create Test Updater Workflow (6 min)

**Step 1: Use cloud agent**

```bash
gh copilot suggest
```

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

**Step 2: Save workflow**

```bash
code .github/workflows/continuous-test-updates.yml
# Paste content
git add .github/workflows/continuous-test-updates.yml
git commit -m "Add continuous test updater"
git push
```

**Step 3: Manually trigger and observe**

**Screen Share:** GitHub Actions → Continuous Test Updates → Run workflow

**While running (2-3 min):**

**Say:**

> "The AI is now:
>
> 1. Scanning all the adventure solution files
> 2. Analyzing which have the least test coverage
> 3. Writing unit tests in the appropriate language
> 4. Creating a pull request
>
> This runs every day. In a month, you'll have 90 new tests without lifting a finger."

### Review Results (3 min)

**Navigate to Pull Requests**

**Show:**

- New PR created by the workflow
- Tests added to specific files
- Descriptive PR description
- Tests follow existing patterns

**Discussion:**

> "What else could you improve continuously? Documentation? Code comments? Refactoring? The pattern is the same: schedule a workflow, make incremental improvements."

**Checkpoint:** "Can everyone see a PR with new tests created?"

---

## Section 5: Exercise 4 - Repository Initialization (1:05-1:15) [10 min]

### Learning Objectives

- Understand `gh aw init` and what it does
- Experience the repository agent (highest quality)
- See the difference between CLI, cloud, and initialized repo approaches

### Introduction (2 min)

**Say:**

> "We've been creating workflows manually. Now let's initialize our repository with `gh aw init`. This sets up the infrastructure and enables the **repository agent**—the highest quality approach. After this, you can use the agentic-workflow-agent right from VS Code or GitHub Copilot chat."

### Initialize Repository (3 min)

**Step 1: Run init command**

```bash
gh aw init
```

**What happens:**

- Creates `.github/aw/` directory
- Sets up configuration files
- Enables repository-aware agent
- Creates activation workflow

**Say:**

> "Now our repository is 'agentic-aware.' The agent understands our workflows, our codebase, and can create contextually relevant automations."

**Step 2: Verify initialization**

```bash
# Check created files
ls -la .github/aw/

# View configuration
cat .github/aw/config.yml
```

**Point out:**

- `config.yml` - Repository-level settings
- `tools/` - Custom tool definitions
- `schemas/` - Validation schemas

**Step 3: Commit init files**

```bash
git add .github/aw/
git commit -m "Initialize GitHub Agentic Workflows"
git push
```

### Use Repository Agent (5 min)

**Step 1: Open VS Code Copilot Chat**

**Screen Share:** VS Code with Copilot Chat panel

**Type in chat:**

```
@agentic-workflows create a workflow that keeps the AGENTS.md file up to date.

It should run weekly, review merged pull requests and updated source files since the last run, then open a pull request that keeps AGENTS.md accurate and current.
```

**Say while AI works:**

> "Notice the difference? I don't need to give it instructions on how to create a workflow or reference documentation. The agent already knows:
>
> - Our repository structure
> - Existing workflows
> - The AGENTS.md file location
> - Best practices from initialization
>
> The quality is significantly better."

**Step 2: Review generated workflow**

**Show:**

- More sophisticated logic
- Better context awareness
- References existing files correctly
- Follows repository conventions

**Step 3: Accept and save**

```bash
# Save the workflow file shown by Copilot
git add .github/workflows/maintain-agents-readme.yml
git commit -m "Add AGENTS.md maintenance workflow"
git push
```

### Compare All Three Approaches (1 min)

**Show slide or diagram:**

```
Quality & Sophistication
        ↑
        |
        |        ③ Repository Agent (gh aw init + VS Code)
        |       /
        |      /
        |     ② Cloud Agent (reference docs)
        |    /
        |   /
        |  ① CLI Wizard (basic templates)
        |_________________________→
                            Ease of Use
```

**Say:**

> "Start with the wizard to learn. Use cloud agent for one-off workflows. Initialize your repository and use the agent for ongoing workflow development. Each has its place."

**Checkpoint:** "Everyone should have `.github/aw/` directory and a workflow created via the repository agent."

---

## Section 6: Exercise 5 - Repository Assistant & Issue Management (1:15-1:30) [15 min]

### Learning Objectives

- Recognize when complexity requires automation
- Implement issue management workflows
- Use discussions for different types of communication

### Introduction (2 min)

**Say:**

> "By now, you might have noticed something: we're creating a lot of issues. Daily standups, CI failures, test PRs generating discussions... it's getting messy. This is actually intentional—it teaches an important lesson: **As your automation grows, you also need automation to manage the automation.**
>
> Let's add a repository assistant to help manage issues."

### Create Repository Assistant (6 min)

**Step 1: Use repository agent in VS Code**

**Copilot Chat:**

```
@agentic-workflows I'm noticing that my issues are growing overwhelming with all these workflow-generated issues. Create a repository assistant workflow that:

1. Runs daily
2. Reviews all open issues
3. Categorizes them (bugs, features, maintenance, automation-generated)
4. Closes stale automation issues (like old daily standups)
5. Prioritizes issues that need human attention
6. Creates a summary issue: "Repository Health Dashboard"
7. Suggests which issues should be moved to Discussions

The assistant should be helpful and respect issues created by humans vs automation.
```

**Say while waiting:**

> "The repository agent understands our issue structure because it has access to the repository context."

**Step 2: Save and deploy**

```bash
git add .github/workflows/repository-assistant.yml
git commit -m "Add repository assistant for issue management"
git push
```

**Step 3: Trigger and observe**

**Screen Share:** Actions tab → Repository Assistant → Run workflow

**Show** (when complete):

- Issues closed/categorized
- New "Repository Health Dashboard" issue
- Suggestions for discussion topics

### Add Issue Triage (4 min)

**Say:**

> "Now let's add automatic triage for new issues. When someone creates an issue, the AI will analyze it, add labels, and suggest priority."

**Copilot Chat:**

```
@agentic-workflows create an issue triage workflow that runs when issues are opened. It should:

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

**Save and deploy:**

```bash
git add .github/workflows/issue-triage.yml
git commit -m "Add automatic issue triage"
git push
```

### Move Issues to Discussions (3 min)

**Say:**

> "Issues are for actionable work. Discussions are for questions, ideas, and community interaction. Let's automate moving the right content to discussions."

**Copilot Chat:**

```
@agentic-workflows create a workflow that identifies issues that should be discussions instead (questions, brainstorming, general inquiries) and posts a comment suggesting the issue be moved to discussions, with a link to create it in the right category.

This should respect that issues are for actionable items and discussions are for conversations.
```

**Save and deploy.**

### Review the Evolution (1 min)

**Show timeline:**

```
1. Started with simple workflows (daily status)
   ↓
2. Added more workflows (CI coach, test updates)
   ↓
3. Issues grew overwhelming
   ↓
4. Added automation to manage automation (assistant, triage)
   ↓
5. Natural organization emerges (discussions)
```

**Say:**

> "This is the pattern: start simple, add complexity when needed, then add management automation. Your repository becomes self-organizing."

**Checkpoint:** "Everyone should now have issue management workflows running."

---

## Section 7: Exercise 6 - Planning & Feature Development (1:30-1:45) [15 min]

### Learning Objectives

- Use `/plan` command in issues for task breakdown
- Trigger workflows from issue comments
- See end-to-end feature development automation

### Introduction (2 min)

**Say:**

> "Let's see the full development cycle automated. We'll create a feature request issue, use `/plan` to break it down, and watch the workflows orchestrate the development."

### Create Feature Issue (3 min)

**Step 1: Create new issue manually**

**Screen Share:** GitHub Issues → New Issue

**Title:**

```
Add Ruby support to CopilotAdventures
```

**Description:**

```
Currently we have Python, C#, and JavaScript solutions. Add Ruby adventure solutions following the same guidelines and structure as the other languages.

Requirements:
- Create Ruby solutions for at least 3 beginner adventures
- Follow the existing naming conventions
- Add README for Ruby setup instructions
- Ensure solutions produce the same output as other languages
```

**Step 2: Watch issue triage run**

**Say:**

> "Our issue triage workflow should kick in automatically. Watch what happens..."

**Show:**

- Workflow triggers
- Labels added automatically
- Complexity estimated
- Comment posted with analysis

### Use /plan Command (5 min)

**Step 1: Comment on the issue**

**Type in issue comment:**

```
/plan
```

**Say:**

> "The `/plan` command is magical. It triggers a workflow that uses AI to break down this feature into actionable tasks."

**Step 2: Watch planning workflow**

**Show:**

- Workflow runs (check Actions tab)
- AI analyzes the feature request
- Creates step-by-step implementation plan

**Step 3: Review generated plan**

**Navigate back to issue**

**Point out:**

- Tasks broken down clearly
- Order of implementation
- Dependencies identified
- Estimated effort
- Sub-issues created (if configured)

**Example expected output:**

```
## Implementation Plan

### Task 1: Setup Ruby Environment
- Add Ruby version file (.ruby-version)
- Create Gemfile with dependencies
- Add Ruby to CI/CD pipeline
**Estimated effort:** 2 hours

### Task 2: Port Beginner Adventures to Ruby
- The Clockwork Town of Tempora
- The Magical Forest of Algora
- The Command Center of Stellaris
**Estimated effort:** 6 hours

### Task 3: Documentation
- Create Solutions/Ruby/README.md
- Update main README with Ruby instructions
- Add Ruby examples to CONTRIBUTING.md
**Estimated effort:** 2 hours

### Task 4: Testing & Validation
- Ensure output matches other languages
- Add Ruby to test matrix
- Document any Ruby-specific considerations
**Estimated effort:** 3 hours

**Total estimated effort:** 13 hours
```

### Trigger Development Workflow (4 min)

**Say:**

> "Now let's actually start working on this. We can trigger a development workflow from discussions or issues."

**Step 1: Add development workflow**

**Copilot Chat:**

```
@agentic-workflows create a workflow that triggers when someone comments "/implement" on an issue. The workflow should:

1. Read the issue description and any plans
2. Create a new branch for the feature
3. Implement the first task in the plan
4. Run tests to verify it works
5. Create a draft pull request
6. Comment back on the original issue with progress

This enables iterative development triggered by humans.
```

**Step 2: Deploy workflow**

```bash
git add .github/workflows/implement-from-issue.yml
git commit -m "Add implementation workflow"
git push
```

**Step 3: Trigger it**

**Comment on Ruby issue:**

```
/implement
```

**Watch:** Workflow runs, creates branch, starts implementation

### Discussion (1 min)

**Say:**

> "This is the power of agentic workflows: human guidance with AI execution. You describe what you want, AI breaks it down and starts building it. You review and approve pull requests. The best of both worlds."

**Checkpoint:** "Can everyone see a `/plan` result on their issue?"

---

## Section 8: Exercise 7 - Advanced: Workflow Reuse & Maintenance (1:45-2:00) [15 min]

### Learning Objectives

- Reuse workflows from other repositories
- Implement automatic workflow maintenance
- Understand workflow evolution and updates

### Introduction (2 min)

**Say:**

> "You don't have to build everything from scratch. GitHub has a library of workflow patterns you can reuse. And more importantly, you can automatically keep them updated."

### Discover & Reuse Workflows (5 min)

**Step 1: Browse workflow library**

**Screen Share:** Browser → https://github.com/githubnext/agentics

**Say:**

> "The githubnext/agentics repository has dozens of pre-built workflows. Let's add one."

**Step 2: Add workflow from remote**

```bash
# Add documentation maintenance workflow
gh aw add githubnext/agentics/continuous-documentation-updates

# View what was added
cat .github/workflows/continuous-documentation-updates.yml
```

**Say:**

> "This workflow monitors your docs and automatically updates them when code changes. We just inherited battle-tested automation in one command."

**Step 3: Customize if needed**

**Copilot Chat:**

```
@agentic-workflows modify the continuous-documentation-updates workflow to only check markdown files in the Adventures/ directory and create PRs labeled "documentation" and "auto-generated"
```

**Step 4: Deploy**

```bash
git add .github/workflows/continuous-documentation-updates.yml
git commit -m "Add continuous documentation updates"
git push
```

### Automatic Workflow Maintenance (6 min)

**Say:**

> "When you reuse workflows, how do you keep them updated? Manual maintenance? No—let's automate that too."

**Step 1: Create workflow maintenance workflow**

**Copilot Chat:**

```
@agentic-workflows create a workflow called "agentics-maintenance" that:

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

**Step 2: Review generated workflow**

**Point out:**

- Goes beyond simple file sync
- Actually tests compatibility
- Provides human-readable changelog
- Allows review before merging

**Step 3: Deploy**

```bash
git add .github/workflows/agentics-maintenance.yml
git commit -m "Add workflow maintenance automation"
git push
```

**Say:**

> "Now our workflows maintain themselves. When the upstream repository improves a pattern, we automatically get a PR to adopt the improvements."

### Validate Rule Files (3 min)

**Say:**

> "One more thing: let's validate our workflow files haven't gotten corrupted or out of sync."

**Copilot Chat:**

```
@agentic-workflows create a workflow that runs on every push and validates:

1. All workflow YAML files are valid
2. Workflows follow agentic best practices
3. Required secrets are defined
4. Workflows don't have conflicting triggers
5. safe-outputs are used correctly

Post a status check that must pass before PRs can merge.
```

**Deploy:**

```bash
git add .github/workflows/validate-workflows.yml
git commit -m "Add workflow validation"
git push
```

### Final Architecture Review (4 min)

**Show diagram of complete system:**

```
Repository Architecture
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Daily Operations:
├── Daily Standup Status (9 AM)
├── Continuous Test Updates (daily)
├── Continuous Documentation Updates (daily)
└── Repository Assistant (daily)

Reactive Workflows:
├── Issue Triage (on issue open)
├── CI Coach (on PR open)
├── CI Doctor (on workflow failure)
└── Implementation (on /implement comment)

Planning & Management:
├── Planning Workflow (on /plan comment)
├── Discussion Migration (as needed)
└── Workflow Maintenance (weekly)

Quality & Validation:
├── Workflow Validation (on push)
└── AGENTS.md Maintenance (weekly)

All orchestrated by GitHub Agentic Workflows 🚀
```

**Say:**

> "Look at what we've built in 2 hours:
>
> - ✅ Daily insights without manual work
> - ✅ Continuous improvement autopilot
> - ✅ Self-organizing issue management
> - ✅ AI-assisted feature planning and implementation
> - ✅ Self-maintaining workflow infrastructure
>
> This is the future of development: humans provide direction, AI handles execution."

**Checkpoint:** "Everyone should have a comprehensive agentic workflow system running."

---

## Section 9: Wrap-up & Q&A (2:00-2:15) [15 min]

### Retrospective (5 min)

**Facilitate discussion:**

"Let's reflect on what we learned. I'll ask a few questions:

1. **What surprised you most** about GitHub Agentic Workflows?
2. **What's one workflow** you're excited to add to your own projects?
3. **What concerns** do you have about using AI automation in production?
4. **How would this change** your team's development process?"

**Take notes on a whiteboard/screen share:**

- Surprises
- Concerns
- Ideas

### Key Takeaways (3 min)

**Review the progression we learned:**

**SLIDE: Key Learnings**

1. **Start Simple → Grow Complex**
   - Begin with obvious automation wins
   - Add complexity when it's clearly needed
   - Don't over-engineer early

2. **Three Approaches, Three Quality Levels**
   - CLI wizard: Learning and simple tasks
   - Cloud agent: Production quality workflows
   - Repository agent: Context-aware excellence

3. **Automation Requires Automation Management**
   - As workflows grow, add orchestration
   - Self-organizing systems emerge naturally
   - Meta-workflows maintain the system

4. **Human-in-the-Loop is Key**
   - AI proposes, humans decide
   - Approval gates for critical operations
   - Review all auto-generated PRs

5. **Natural Language is Powerful**
   - Describe what you want, not how to do it
   - Reference documentation URLs for better results
   - Iterate by refining descriptions

### Best Practices & Guardrails (3 min)

**SLIDE: Safety First**

**Do:**

- ✅ Start with read-only workflows
- ✅ Use safe-outputs for all writes
- ✅ Add human approval for critical operations
- ✅ Monitor workflow runs regularly
- ✅ Version control all workflow files
- ✅ Test workflows on private repos first

**Don't:**

- ❌ Give workflows admin permissions
- ❌ Auto-merge workflow PRs without review
- ❌ Use workflows on public repos with sensitive data
- ❌ Blindly trust AI-generated code
- ❌ Skip security reviews
- ❌ Forget to set spending limits on Actions

### Next Steps & Resources (2 min)

**SLIDE: Continue Learning**

**Your Repository:**

- Keep experimenting with your CopilotAdventures repository
- Try adding workflows for your own projects
- Share your creations with the community

**Resources:**

- 📖 Documentation: https://github.github.com/gh-aw/
- 🏭 Peli's Agent Factory: https://github.github.com/gh-aw/blog/2026-01-12-welcome-to-pelis-agent-factory/
- 💬 Community: https://github.com/orgs/community/discussions/186451
- 🎮 Discord: https://gh.io/next-discord
- 📦 Workflow Library: https://github.com/githubnext/agentics
- 🎓 CopilotAdventures: https://github.com/microsoft/CopilotAdventures

**Join the Community:**

- Share your workflows in GitHub Discussions
- Contribute to githubnext/agentics
- Attend GitHub Copilot Dev Days events

### Open Q&A (5 min)

**Field questions on:**

- Technical implementation details
- Use case specifics
- Troubleshooting setup issues
- Integration with existing tools
- Enterprise/team considerations
- Security and compliance
- Cost and billing

**Common Questions & Answers:**

**Q: "How much does this cost?"**
A: "Workflows run on GitHub Actions minutes. Typically very low cost—most workflows run in <5 minutes. Set spending limits in Settings."

**Q: "Can this work with private repositories?"**
A: "Yes! In fact, we recommend testing on private repos first. All the same features work."

**Q: "What if the AI makes a mistake?"**
A: "That's why we have PR reviews and approval gates. Always review auto-generated code before merging."

**Q: "Can I use this with other CI/CD tools?"**
A: "G workflows run on GitHub Actions, but they can trigger other systems or be triggered by webhooks from external tools."

**Q: "How do I get my team on board?"**
A: "Start small—add one workflow that solves a clear pain point. Let the value speak for itself."

**Q: "Does this replace developers?"**
A: "No! It amplifies developers. You describe what you want, review the results, and make decisions. AI handles the repetitive execution."

### Closing (1 min)

**Say:**

> "Thank you all for participating! You now have:
>
> - A working agentic workflow system ✓
> - The knowledge to build more ✓
> - A repository you can continue using ✓
> - Access to a community of practitioners ✓
>
> The future of development isn't humans vs AI—it's humans directing AI to handle the repetitive work while we focus on the creative and strategic. You're now equipped to build that future.
>
> Please fill out the feedback survey [show link/QR code], connect with each other, and keep experimenting. See you at the next GitHub Copilot Dev Days event!"

**Final logistics:**

- Share survey link
- Share your contact info for follow-up questions
- Let people know about upcoming events
- Encourage attendees to share their creations

---

## Post-Workshop

### Immediate Follow-up (within 24 hours)

- [ ] Send thank you email with resources
- [ ] Share link to workshop recording (if recorded)
- [ ] Post summary to GitHub Discussions
- [ ] Respond to feedback survey comments
- [ ] Share attendee-created workflows (with permission)

### Analysis (within 1 week)

- [ ] Review feedback survey results
- [ ] Identify common pain points to address next time
- [ ] Update facilitator guide with lessons learned
- [ ] Share anonymized insights with GitHub Copilot Dev Days organizers

### Community Building

- [ ] Create GitHub Discussion for workshop alumni
- [ ] Schedule optional office hours for follow-up questions
- [ ] Highlight interesting workflows created by attendees
- [ ] Consider advanced workshop for returning attendees

---

## Troubleshooting Guide

### Common Issues During Workshop

**Issue: `gh aw` command not found**

- **Cause:** Extension not installed or not in PATH
- **Fix:** `gh extension install github/gh-aw` and ensure gh CLI is updated

**Issue: Authentication fails**

- **Cause:** Network restrictions or expired token
- **Fix:** Use `gh auth refresh` or try browser-based auth alternative

**Issue: Workflows not triggering**

- **Cause:** Permissions not set correctly
- **Fix:** Check Settings → Actions → Permissions (read/write required)

**Issue: COPILOT_GITHUB_TOKEN secret invalid**

- **Cause:** Token doesn't have copilot scope or expired
- **Fix:** Regenerate token with proper permissions, verify expiration date

**Issue: "Repository not initialized" error when using agent**

- **Cause:** Forgot to run `gh aw init`
- **Fix:** Run `gh aw init` and commit changes

**Issue: Workflow runs but fails immediately**

- **Cause:** Usually YAML syntax error or missing secret
- **Fix:** Check Actions logs for specific error, validate YAML

**Issue: PR not created by workflow**

- **Cause:** "Allow GitHub Actions to create PRs" not enabled
- **Fix:** Settings → Actions → Workflow permissions → Enable

**Issue: Participant can't create/clone repository**

- **Cause:** Network/firewall restrictions
- **Fix:** Use GitHub Codespaces as alternative environment

---

## Facilitator Tips

### Energy Management

- Take a 5-minute break at the 1-hour mark
- Use humor when appropriate (AI can be quirky)
- Celebrate when workflows work correctly
- Stay calm when demos fail (they will)

### Pacing

- Watch for lost participants (roving help during exercises)
- Use checkpoints to ensure everyone's together
- Skip optional sections if running behind
- Extend Q&A if finishing early

### Engagement

- Ask questions throughout (not just at end)
- Invite participants to share screens when successful
- Create a "wins" channel for people to share results
- Pair struggling participants with successful ones

### Adaptability

- Have backup examples if live demos fail
- Prepare for different skill levels in audience
- Be ready to skip advanced sections if needed
- Keep enthusiasm high even when things break

---

## Materials Checklist

### Digital Assets

- [ ] Slide deck (introduction presentation)
- [ ] Participant handout (command reference)
- [ ] Example repository with working workflows
- [ ] Backup PAT tokens (for emergencies)
- [ ] Pre-recorded demo videos (backup)
- [ ] Feedback survey link/QR code

### Physical Materials

- [ ] Power strips/extension cords
- [ ] HDMI/display adapters
- [ ] Printed handouts (optional)
- [ ] Sticky notes for questions
- [ ] Whiteboard markers
- [ ] Workshop signs/room indicators

### Technical Setup

- [ ] Test projector/screen connection
- [ ] Verify WiFi capacity
- [ ] Have mobile hotspot as backup
- [ ] Test all demo workflows day before
- [ ] Charge laptop fully
- [ ] Have backup laptop ready

---

**Version:** 1.0  
**Last Updated:** March 4, 2026  
**Facilitator:** [Your Name]  
**Event:** GitHub Copilot Dev Days 2026
