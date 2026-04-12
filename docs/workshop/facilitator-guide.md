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

| Time | Section                              | Duration | Activity                              |
| ---- | ------------------------------------ | -------- | ------------------------------------- |
| 0:00 | Intro & Welcome                      | 15 min   | Presentation                          |
| 0:15 | Setup                                | 15 min   | Installation, Config & CI Pipeline    |
| 0:30 | Exercise 1: Daily Status             | 10 min   | First workflow with CLI               |
| 0:40 | Exercise 1b: Upgrade Daily Report    | 10 min   | Cloud agent upgrade                   |
| 0:50 | Exercise 2: CI Coach                 | 15 min   | Manual creation + `gh aw init`        |
| 1:05 | Exercise 3: CI Doctor                | 15 min   | Manual creation + testing             |
| 1:20 | Exercise 4: Continuous Test Updates  | 10 min   | Cloud agent creation                  |
| 1:30 | Exercise 5: Repository Agent         | 10 min   | VS Code agent workflow                |
| 1:40 | Exercise 6: Issue Triage             | 10 min   | Reusing community workflows           |
| 1:50 | Exercise 7: Feature Planning         | 10 min   | `/plan` command                       |
| 2:00 | Wrap-up & Q&A                        | 15 min   | Exercise 8 + Retrospective            |

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

**SLIDE 3: How We're Building**

> "You'll experience multiple approaches to creating workflows, each with increasing quality and sophistication."

1. **Interactive CLI** (`gh aw new`)
   - Interactive guided prompts
   - Quick and simple
   - Good for learning
   - Creates .md source and .lock.yml compiled files
   - Basic prompt quality

2. **Manual creation** (paste workflow + `gh aw compile`)
   - Full control over workflow content
   - Teaches the anatomy of agentic workflows
   - Best for understanding frontmatter + natural language prompt structure

3. **Cloud Agent** (web browser agent tab)
   - References documentation automatically
   - Higher quality results
   - Better prompts for complex workflows
   - Creates PRs with workflow changes

4. **Repository Agent** (VS Code Copilot Chat after `gh aw init`)
   - Use `/agents` command and select from UI
   - Best quality results
   - Context-aware of your repository
   - Can reference existing workflows
   - Integrates deeply with Copilot

5. **Community Workflows** (`gh aw add`)
   - Reuse proven, battle-tested workflows
   - One command to install
   - Refined through real-world usage

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

1. Daily status report (CLI + Cloud Agent upgrade)
2. CI Coach (manual creation)
3. CI Doctor (manual creation)
4. Continuous test updates (cloud agent)
5. Repository agent workflow (VS Code)
6. Issue triage (reuse community workflows)
7. Feature planning (/plan command)
8. Explore on your own
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

# Linux (Debian/Ubuntu)
sudo mkdir -p -m 755 /etc/apt/keyrings
wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh -y

# Verify installation
gh --version
# Should show version 2.87.3 or higher
```

```bash
# 2. Install gh copilot extension (optional but recommended for later)
gh extension install github/gh-copilot

# 3. Install gh-aw extension
gh extension install github/gh-aw

# Verify
gh aw --version
# Should show version v0.68.1 or higher
```

**Checkpoint:** "Raise your hand if you see version v0.68.1 or higher for `gh aw`"

### Authentication (3 min)

```bash
# Authenticate with GitHub
gh auth login

# Follow prompts:
# ? Where do you use GitHub? → GitHub.com
# ? What is your preferred protocol for Git operations? → HTTPS  
# ? Authenticate Git with your GitHub credentials? → Yes
# ? How would you like to authenticate GitHub CLI? → Login with a web browser

# Copy the one-time code (e.g., XXXX-XXXX)
# Press Enter to open https://github.com/login/device
# Paste code in browser → Authorize

# Expected output:
# ✓ Authentication complete.
# ✓ Logged in as <username>
```

**Common Issue:** Browser doesn't open

- Manually go to https://github.com/login/device
- Enter code shown in terminal

**Checkpoint:** "Everyone should see 'Logged in as [your-username]'"

### Repository Setup (7 min)

**Step 1: Create new repository**

**Say:** "We'll each create our own repository so you can continue using it after the workshop."

**Screen Share:** GitHub web UI

**Important:** Ensure everyone is signed in to github.com first.

1. Go to github.com → Click **New** (top left, next to "Top Repositories")
2. **Choose owner:** Select your GitHub user account
3. **Name:** `copilot-adventures-[yourname]`
4. **Visibility:** Public or Private (your choice)
5. **Do NOT** add README, .gitignore, or license
6. Click "Create repository"

**Step 2: Configure repository settings**

Navigate to Settings:

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
- **Note:** Feature changes are applied immediately (no save button)

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

1. Click **profile icon** (top-right) → **Settings** → **Developer settings** (bottom left of new page)
2. **Personal access tokens** → **Fine-grained tokens** → Click "**Generate new token**"
3. **Token name:** `Agentic Workflows Copilot Token`
4. **Leave the defaults:**
   - Resource owner: Your GitHub user account
   - Expiration: 30 days
   - Repository access: Public Repositories (only)
5. **Permissions:** Scroll down → Click "**Add permission**" → Select **"Copilot Requests"**
   - Explain: "This allows the token to make Copilot requests on your behalf, using your premium quota"
6. Click "**Generate token**"
7. **Copy token immediately** (won't see it again)

```bash
# Store token in repository secrets
gh aw secrets set COPILOT_GITHUB_TOKEN --value "YOUR_TOKEN_HERE"
```

**Security Note:**

> "Never share this token or commit it to your repository. It's stored securely in GitHub secrets."

**Step 5: Create Classic Token for CI Trigger**

**Say:** "Some agentic workflows create pull requests that should trigger your CI pipeline. For that to work, we need a classic token with `repo` and `workflow` permissions."

1. Go to **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
2. Click "**Generate new token**" → Select **"Generate new token (classic)"**
3. **Note:** `gh-aw-application`
4. **Expiration:** 30 days
5. **Select scopes:**
   - ✅ **repo** (Full control of private repositories)
   - ✅ **workflow** (Update GitHub Action workflows)
6. Click "**Generate token**" → **Copy it immediately**

```bash
# Store the classic token as a repository action secret
gh aw secrets set GH_AW_CI_TRIGGER_TOKEN --value "YOUR_COPIED_TOKEN"
```

**Say:** "Without this classic token, workflows can still create issues, but PRs created by the agent won't automatically trigger CI runs."

**Checkpoint:** "Go to your repository Settings → Secrets → Actions. You should see both **COPILOT_GITHUB_TOKEN** and **GH_AW_CI_TRIGGER_TOKEN** listed."

**Step 6: Add a CI Pipeline**

**Say:** "Before we create agentic workflows, let's add a basic CI pipeline. This will be used later by the CI Coach and CI Doctor workflows."

**Screen Share:** File creation

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-csharp:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.0.x'
      
      - name: Build C# Solutions
        run: dotnet build Solutions/CSharp/CopilotAdventures.sln
  
  build-javascript:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      
      - name: Validate JavaScript Files
        run: |
          for f in Solutions/JavaScript/*.js; do node --check "$f"; done
          echo "JavaScript syntax validation passed"
  
  build-python:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'
      
      - name: Validate Python Files
        run: |
          python -m py_compile Solutions/Python/*.py
          echo "Python syntax validation passed"
```

```bash
git add .github/workflows/ci.yml
git commit -m "Add CI build pipeline"
git push
```

**Say:** "This pipeline only builds and validates syntax—no tests yet. The CI Coach will later analyze this pipeline and suggest improvements."

### Setup Complete (1 min)

**Say:**

> "Great! Setup is done. Now we have:
>
> - GitHub CLI with gh-aw extension ✓
> - Our own copy of CopilotAdventures ✓
> - Repository properly configured ✓
> - Copilot token and CI trigger token stored ✓
> - Basic CI pipeline running ✓
>
> Time to build some workflows!"

---

## Section 2: Exercise 1 - Daily Status Report (0:30-0:40) [10 min]

### Learning Objectives

- Create first workflow using interactive CLI (`gh aw new`)
- Understand workflow structure (.md source and .lock.yml compiled)
- Learn about frontmatter and natural language instructions
- Understand supporting files (.gitattributes, actions-lock.json)
- See workflow run and produce results
- Recognize limitations of basic prompts (setup for future exercises)

### Introduction (2 min)

**Say:**

> "Before we dive into creating workflows, let's talk about why we're here. Imagine your team of 9 people working on this repository. You have daily standups and progress boards, but what happens when someone has a day off? Who notices that PR sitting open for 2 days without a review? Who remembers to mention everything during standup?
> 
> Instead of relying solely on humans to track everything, we're going to create automated assistants that work 24/7. They never forget, never take days off, and always provide objective data about what's happening in your repository.
>
> Let's start with the most fundamental need: knowing what happened in your repository each day. We'll create a daily standup report that runs every morning at 9 AM."

### Live Code-Along (6 min)

**Step 1: Create workflow using interactive CLI**

```bash
gh aw new
```

💡 **Note:** This command launches an interactive mode that guides you through creating a workflow.

**Guide through the prompts:**

**1. What should we call this workflow?**
```
daily-report
```

**2. When should this workflow run?**
- Show options and select: `Schedule (daily, scattered execution time)`

**3. Which AI engine should process this workflow?**
- Show options and select: `copilot - GitHub Copilot CLI`

**4. Which tools should the AI have access to?**
- Navigate and select: `github` - GitHub API tools (issues, PRs, comments, repos)
- Point out the tools it enables:
  - `create-issue` - Create a new GitHub issue
  - `add-comment` - Add a comment to an issue, PR, or discussion
  - `close-issue` - Close a GitHub issue
  - `update-issue` - Update an existing GitHub issue

**5. Network Access Control**
- Leave defaults (arrow down to continue)

**Say:** "For this workflow, we don't need external network access. The AI will only use GitHub's API."

**6. What should this workflow do?**
```
Run daily at 9 AM and create an issue with a summary of repository activity from past 24 hours. Include commits, pull requests, issues, and CI/CD failures.
```

**Say while it compiles:**

> "The system is now compiling your workflow. This takes your natural language description and creates the actual GitHub Actions workflow files."

**Step 2: Review the generated files**

**Say:**

> "Notice it created FOUR files. Let's look at what was generated."

```bash
# List the workflow files
ls -la .github/workflows/

# Review the markdown source
cat .github/workflows/daily-report.md

# Review the compiled lock file
cat .github/workflows/daily-report.lock.yml
```

**Point out the four generated files:**

1. **`daily-report.md`** in `.github/workflows/` - The editable source workflow
2. **`daily-report.lock.yml`** in `.github/workflows/` - The compiled GitHub Actions workflow
3. **`.gitattributes`** in the repository root - Git configuration for lock files
4. **`.github/aw/actions-lock.json`** - GitHub Actions version lock file

**Explain `daily-report.md`:**

- **Frontmatter** (between `---` markers):
  - `on: schedule` - When it runs
  - `permissions` - What it can access
  - `tools` - Capabilities (create-issue, etc.)
- **Natural language instructions** below the frontmatter

**Explain `daily-report.lock.yml`:**

- This is the compiled GitHub Actions workflow
- Contains a simplified version of your prompt
- This is what GitHub Actions actually executes
- Gets regenerated when you edit the `.md` file

**Explain `.gitattributes`:**

- Marks `.lock.yml` files as generated (excluded from language statistics)
- Sets merge strategy to `ours` (automatically resolves merge conflicts)

**Explain `.github/aw/actions-lock.json`:**

- Locks GitHub Actions to specific versions and commit SHAs for security
- Cache of resolved `action@version` → commit SHA mappings
- Commit this file so all contributors use consistent action references

**Say:**

> "The `.md` file is your source of truth - you edit this one. The `.lock.yml` file is compiled from it. Always commit all files together."

📚 **Reference:** Point participants to [How Agentic Workflows Work](https://github.github.com/gh-aw/introduction/how-they-work/)

**Step 3: Observe the limitation (Important setup for next exercises)**

**Say:**

> "Now here's something important: look at the prompt inside the .lock.yml file. It's very basic - just the description we typed. This will work, but the quality depends heavily on your prompt. A simple one-sentence description means the AI might miss details, format inconsistently, or lack proper error handling.
> 
> This is perfectly fine for learning, but in the next exercises, we'll use more sophisticated approaches that generate much better prompts and higher-quality workflows. Think of this as 'Workflow Creation 101' - simple but limited."

**Step 4: Commit and push**

```bash
# Commit all generated files
git add .
git commit -m "Add daily report workflow (basic version)"
git push
```

### Trigger and Review (2 min)

**Step 5: Trigger manually for demo**

**Say:** "Since it's scheduled for 9 AM daily, let's trigger it manually now to see it work."

**Screen Share:** GitHub Actions tab

1. Navigate to Actions tab
2. Find "daily-report" workflow in the list
3. Click "Run workflow" button → Run workflow
4. Watch it execute (usually 1-2 minutes)

**While waiting, explain the 5 execution phases:**

> "The workflow runs through 5 distinct phases:
>
> 1. **activation** (~16s) - Sets up the environment and checks out repository code
> 2. **agent** (~2m) - The AI agent analyzes your repository and formulates a summary
> 3. **detection** (~45s) - Validates the agent's output is properly formatted and safe
> 4. **safe_outputs** - Interprets the JSON output and creates the actual issue
> 5. **conclusion** - Finalizes and cleans up
>
> Important: The agent itself doesn't directly create issues. It produces structured JSON output that the `safe_outputs` step interprets to make the actual GitHub API calls. This separation ensures security."

### Review Results (1 min - if time permits)

**Navigate to Issues tab**

**Point out if the issue was created:**

- New issue with repository summary
- Note the format and content
- Explain it will run automatically every day at 9 AM

**Transition to next exercise:**

> "Great! We've created our first workflow. In the next exercise, we'll upgrade this using the cloud agent, which produces much higher quality workflows by referencing official documentation. Let's see the difference."

**Checkpoint:** "Everyone should have all workflow files committed and pushed. Raise your hand if you need help or if your workflow is still running."

---

## Section 3: Exercise 1b - Upgrade Daily Report with Cloud Agent (0:40-0:50) [10 min]

### Learning Objectives

- Use the cloud agent for higher quality workflow generation
- Understand why documentation reference produces better prompts
- Experience the PR-based workflow update process
- Compare basic CLI output vs cloud agent output

### Introduction (2 min)

**Say:**

> "In Exercise 1, you used the interactive CLI to create a daily-report workflow. It works, but the prompt is minimal—just your one-line description. The cloud agent produces significantly better workflows because it can **download and reference the official documentation** while generating the workflow.
>
> Think of it this way: the CLI is like writing a quick note from memory, while the cloud agent is like writing with the documentation open in front of you."

### Upgrade Using Cloud Agent (6 min)

**Step 1: Navigate to the cloud agent**

**Screen Share:** GitHub web UI

**Guide participants:**

1. Go to your repository on GitHub.com in your web browser
2. Click on the **Agent** tab (next to Code, Issues, Pull Requests, etc.)

**⚠️ First-time setup — Configure billing for cloud resources:**

**Say:** "If this is your first time using the cloud agent, you may see a red banner about billing. Let me walk you through configuring it."

1. Click the link in the banner, or navigate: **Profile icon** → **Settings** → **Copilot** → **Features**
2. Scroll to **Billing** section
3. Under **"Usage billed to"**, click **"Select billing entity"**
4. Select the **organization** where you receive your Copilot license from
5. Return to repository and click the **Agent** tab again

**Step 2: Provide the upgrade prompt**

**Say:** "We're going to ask the cloud agent to upgrade our existing daily-report workflow and create a PR with the changes."

**Prompt:**

```
Update the existing daily-report workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md. Create a Pull Request when you're done.

The purpose of the workflow is to act as a daily report that helps team members keep up to date. It should:
Run daily at 9 AM and create an issue with a summary of repository activity from past 24 hours. Include commits, pull requests, issues, and CI/CD failures.

Use the schedule trigger and create issues using safe-outputs.
```

**Say while AI generates:**

> "Notice we're referencing the URL to the creation guide. This means the AI can reference the exact patterns and best practices from the official docs. The quality is much better than the simple interactive CLI approach."

**Step 3: Review and merge the generated PR**

1. Go to **Pull Requests** tab
2. Review the PR created by the agent
3. **Compare the changes:** Show how the cloud agent improved the prompt in `daily-report.md`
4. Verify both workflow files are updated
5. **Merge the PR to main**

```bash
git pull
```

**Step 4: Compare the improvement**

**Say:**

> "Open the updated `daily-report.md` and notice how much richer the prompt is. The cloud agent typically adds structured output formatting, specific sections for different activity types, error handling guidance, and tone direction."

### Trigger and Compare (2 min)

**Step 5: Trigger the upgraded workflow**

1. Go to **Actions** tab → **daily-report** → **Run workflow**
2. Watch it execute through the same 5 phases

**Say:**

> "The resulting issue should be better structured and formatted. Same information, dramatically better instructions. This is why we use the cloud agent for subsequent exercises."

**Key Takeaway:**

> "The quality of the AI's output depends on the quality of the instructions. Richer prompts from the cloud agent mean more consistent, reliable results."

**Checkpoint:** "Everyone should have the upgraded daily-report merged. Let's continue."

---

## Section 4: Exercise 2 - CI Coach (0:50-1:05) [15 min]

### Learning Objectives

- Understand `gh aw init` and what it does
- Create a workflow file manually to learn the anatomy
- Understand frontmatter configuration vs natural language prompt
- Use `gh aw compile` to generate the lock file
- Experience the branch → PR → merge workflow

### Introduction (2 min)

**Say:**

> "Now that you have visibility into daily activity, let's focus on the backbone of your validation system: your CI pipeline. Your CI pipeline triggers on each change, validates each update, and deploys to customers. Teams often set up CI once and then the codebase evolves without the pipeline keeping pace.
>
> Instead of waiting for CI to fail and then reacting, we'll create a CI Coach that provides proactive guidance. This time, we'll create the workflow file manually—this teaches you the anatomy of an agentic workflow so you understand exactly what the CLI and cloud agent generate for you."

### Initialize Agentic Workflows (3 min)

**Step 1: Run init command**

**Say:** "In Exercise 1, `gh aw new` handled initialization for you. But now that we're creating a workflow manually, we need to initialize the agentic workflows tooling explicitly. This sets up the `copilot-setup-steps.yml` file that configures the MCP server powering the AI agent."

```bash
gh aw init
```

**What happens:**

- Creates `.github/aw/` directory
- Sets up configuration files including `copilot-setup-steps.yml`
- Enables repository-aware agent capabilities

**Step 2: Verify initialization**

```bash
ls -la .github/aw/
```

**Say:** "Without this initialization, compiled workflows won't have the infrastructure to run the agent and process safe-outputs."

### Create CI Coach Manually (8 min)

**Step 2: Create a branch**

```bash
git pull
git checkout -b add-ci-coach
```

**Step 3: Create the workflow file**

**Say:** "We're going to create `.github/workflows/ci-coach.md` manually. This is the same format the CLI and cloud agent generate—frontmatter configuration plus a natural language prompt."

**Screen Share:** Show participants creating the file in their editor.

**Walk through the key parts of the workflow as participants paste it:**

**Explain the frontmatter:**

- `on: schedule` + `workflow_dispatch` — Runs daily and can be triggered manually
- `permissions: read-all` — Agent can read everything but writes only through safe-outputs
- `tools:` — GitHub API, bash, and web-fetch capabilities
- `safe-outputs: create-pull-request:` — Agent creates PRs (not direct changes) with `[ci-coach]` title prefix
- `engine: copilot` — Uses GitHub Copilot as the AI engine

**Explain the natural language prompt:**

- 5-phase analysis framework (Discovery → Analysis → Prioritization → Implementation → No Changes Path)
- Optimization patterns and anti-patterns
- PR template for consistent output
- Quality standards and success criteria

**Say:**

> "Notice how detailed and structured this is compared to the basic prompt from Exercise 1. The 5-phase framework, optimization patterns, anti-patterns, and PR template all guide the agent toward consistent, high-quality results. The quality of the prompt directly determines the quality of the agent's output."

**Step 4: Compile the workflow**

```bash
gh aw compile ci-coach
```

**Say:** "This generates the `.lock.yml` file—the compiled GitHub Actions workflow that actually executes."

**Step 5: Commit and push**

```bash
git add .
git commit -m "Add CI Coach optimization workflow"
git push -u origin add-ci-coach
```

**Step 6: Create a PR and merge**

```bash
gh pr create --title "Add CI Coach workflow" --body "Daily CI optimization coach that analyzes workflows for efficiency improvements and cost reduction opportunities"
```

1. Review the PR on GitHub
2. Merge to main

```bash
git checkout main
git pull
```

### Trigger and Iterate (2 min)

**Step 7: Trigger the workflow**

1. Go to **Actions** tab → **ci-coach** → **Run workflow**
2. Watch it execute through the 5 phases

**Say:**

> "The CI Coach will analyze your CI pipeline and create a PR with suggested improvements. On the first run it might propose caching or parallelization. You may need to merge and re-trigger a few times to get it to add tests to the CI pipeline—each run builds on previous improvements."

**Key Insight:**

> "By creating this workflow manually, you now understand exactly what the CLI and cloud agent generate behind the scenes. Every agentic workflow is just a markdown file with frontmatter configuration plus a natural language prompt."

**Checkpoint:** "Everyone should have the CI Coach workflow merged to main. Let's continue."

---

## Section 5: Exercise 3 - CI Doctor (1:05-1:20) [15 min]

### Learning Objectives

- Create another manual workflow with different triggers
- Understand label_command triggers vs schedule triggers
- Experience testing a workflow with intentional breakage
- See the full diagnosis and remediation cycle

### Introduction (2 min)

**Say:**

> "Think about your team's current workflow when something breaks in CI. Someone gets a notification, stops their current work to investigate, digs through logs, searches for fixes. This constant context switching is expensive.
>
> The CI Doctor eliminates that. It activates when you add the `ci-doctor` label to a PR with failing checks, analyzes the failure logs, and posts a diagnostic comment with actionable fixes. Let's create it manually, just like the CI Coach."

### Create CI Doctor Manually (7 min)

**Step 1: Create a branch**

```bash
git checkout main
git pull
git checkout -b add-ci-doctor
```

**Step 2: Create the workflow file**

**Say:** "Create `.github/workflows/ci-doctor.md` and paste the workflow content."

**Walk through the key differences from CI Coach:**

- **Trigger**: `label_command` instead of `schedule` — activates when you add the `ci-doctor` label to a PR
- **Permissions**: Granular read-only permissions for actions, contents, issues, PRs, and checks
- **safe-outputs**: Creates issues (not PRs) with `[CI Failure Doctor]` prefix, and comments on PRs
- **steps**: Pre-processing bash scripts that download failure logs and artifacts *before* the AI agent starts
- **Two modes**: PR Check Review (label-triggered) and CI Failure Investigation (workflow_run-triggered)

**Say:**

> "Notice the pre-processing steps. The workflow downloads logs and artifacts before the AI agent starts, giving it pre-filtered data to work with. This is a pattern for workflows that need to analyze large amounts of data efficiently."

**Step 3: Compile the workflow**

```bash
gh aw compile ci-doctor
```

**Step 4: Commit and push**

```bash
git add .
git commit -m "Add CI Doctor diagnostic workflow"
git push -u origin add-ci-doctor
```

**Step 5: Create a PR and merge**

```bash
gh pr create --title "Add CI Doctor workflow" --body "CI failure diagnostician that investigates failing checks and posts actionable diagnosis"
```

1. Review and merge the PR
2. Return to main:

```bash
git checkout main
git pull
```

### Test with Intentional Breakage (4 min)

**Step 6: Create a failing PR**

**Say:** "To see the CI Doctor in action, let's intentionally break the build."

```bash
git checkout -b test/trigger-ci-doctor
echo "this is not valid javascript %%%" >> Solutions/JavaScript/The-Clockwork-Town-of-Tempora.js
git add .
git commit -m "Test: Intentionally break build to trigger CI Doctor"
git push -u origin test/trigger-ci-doctor
gh pr create --title "Test: Trigger CI Doctor" --body "Intentionally breaking a build to demonstrate the CI Doctor workflow"
```

**Step 7: Trigger the CI Doctor**

1. Wait for CI to **fail** (red ❌) on the PR
2. Add the **`ci-doctor`** label to the PR
3. Go to **Actions** tab and watch the `ci-doctor` workflow execute
4. Return to the PR — the CI Doctor posts a **diagnostic comment** with:
   - Summary of failing checks
   - Root cause analysis
   - Specific recommended fixes with file paths
   - Prevention tips

**Say while waiting:**

> "The CI Doctor is reading the failure logs, identifying the root cause, and preparing a diagnosis. Notice how it provides actionable fixes, not just a description of the problem."

### Clean Up and Review (2 min)

**Step 8: Show the diagnostic output**

**Point out:**

- Structured diagnosis with sections
- Specific file paths and line numbers
- Recommended fixes
- Prevention strategies

**Say:**

> "You can also ask Copilot to fix it by commenting `@copilot fix the issue` on the PR. Copilot uses the CI Doctor's diagnosis as context."

**Clean up the test branch:**

```bash
git checkout main
gh pr close test/trigger-ci-doctor
git branch -D test/trigger-ci-doctor
git push origin --delete test/trigger-ci-doctor
```

**Key Insight:**

> "Your DevOps guardrails are now stronger: you have visibility (Exercise 1), proactive coaching (Exercise 2), and automated diagnosis (Exercise 3). These workflows work together to keep your repository healthy with minimal human intervention."

**Checkpoint:** "Everyone should have the CI Doctor working. Let's continue."

---

## Section 6: Exercise 4 - Continuous Test Updates (1:20-1:30) [10 min]

### Learning Objectives

- Use the cloud agent for consistent quality workflow creation
- Understand the continuous improvement pattern
- See AI making incremental code changes via PRs

### Introduction (2 min)

**Say:**

> "Every team knows tests are important, but writing comprehensive coverage is time-consuming, tedious, and often deprioritized. Instead of one big push, why not add 3 tests every day automatically? Over time, your coverage improves without any manual effort.
>
> 3 tests per day = ~1,000 tests per year. That's sustainable background improvement."

### Create Test Updater via Cloud Agent (5 min)

**Step 1: Use cloud agent**

**Guide participants:**

1. Go to your repository on GitHub.com
2. Click on the **Agent** tab
3. Enter the following prompt:

**Prompt:**

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md, create a pr when your done

The purpose of the workflow is to continuously improve test coverage. It should run daily and:
1. Analyze the codebase to find 3 files with missing or inadequate tests
2. Generate meaningful unit tests for those files
3. Ensure tests follow the existing test conventions in the repository
4. Create a pull request with the new tests
5. Limit to 3 test additions per day to keep PRs manageable

The workflow should work across C#, JavaScript, and Python files in the Solutions/ directory.

Use a daily schedule trigger and create PRs with safe-outputs.
```

**Step 2: Review and merge the generated PR**

1. Go to **Pull Requests** tab
2. Review the PR with the workflow files:
   - `.github/workflows/continuous-test-updates.md`
   - `.github/workflows/continuous-test-updates.lock.yml`
3. **Merge the PR to main**

```bash
git pull
```

### Trigger and Review (3 min)

**Step 3: Manually trigger the workflow**

**Screen Share:** GitHub Actions → continuous-test-updates → Run workflow

**While running:**

**Say:**

> "The AI is now scanning solution files, analyzing which have the least test coverage, writing unit tests in the appropriate language, and creating a pull request. This runs every day—in a month, you'll have 90 new tests without lifting a finger."

**Step 4: Review the results**

**Navigate to Pull Requests**

**Show:**

- New PR created by the workflow
- Tests added to specific files
- Descriptive PR description
- Tests follow existing patterns

**Discussion:**

> "By generating 3 tests per day, you build robust test coverage without disrupting feature development. Better tests mean better AI outcomes—the more validation you have, the safer it is to let AI make autonomous changes."

**Checkpoint:** "Can everyone see a PR with new tests created? Let's continue."

---

## Section 7: Exercise 5 - Create Workflow with Repository Agent (1:30-1:40) [10 min]

### Learning Objectives

- Use the repository agent directly in VS Code
- Experience the highest quality workflow creation approach
- Understand protected files and fallback-to-issue pattern
- Stay in the IDE for the full workflow creation cycle

### Introduction (2 min)

**Say:**

> "So far, you've created workflows using the interactive CLI, manual creation, and the cloud agent. But most developers spend their time in VS Code, not on GitHub.com. Every context switch costs focus.
>
> Remember the `gh aw init` you ran in Exercise 2? That configured the repository agent. Now you can use GitHub Copilot Chat directly in VS Code to create agentic workflows—no browser needed. This is the most practical method for ongoing workflow development."

### Create AGENTS.md Maintenance Workflow (6 min)

**Step 1: Create a branch**

```bash
git checkout main
git pull
git checkout -b workflow/agents-md-maintenance
```

**Step 2: Use the repository agent in VS Code**

**Screen Share:** VS Code with Copilot Chat panel

1. **Open Copilot Chat**
2. Type `/agents` to view available agents
3. Select the **agentic-workflows** agent from the UI

**Type the prompt:**

```
create a workflow that keeps the AGENTS.md file up to date.

It should run weekly, review merged pull requests and updated source files since the last run, then open a pull request that keeps AGENTS.md accurate and current.

make sure to allow the agents.md file, as it is an a protected file
---
    allowed-files: ["AGENTS.md"]
    protected-files: fallback-to-issue
---
```

**Say while AI works:**

> "Notice the difference with the repository agent? After selecting it from `/agents`, I don't need to reference documentation URLs. The agent already knows our repository structure, existing workflows, and best practices from initialization. The quality is significantly better.
>
> When Copilot asks to fetch a web reference, choose allow. Same for compiling the workflow."

**Step 3: Compile, commit, and create PR**

```bash
# Compile the workflow
gh aw compile agents-md-maintenance

# Add both files
git add .

# Commit
git commit -m "Add AGENTS.md maintenance workflow"

# Push the branch
git push -u origin workflow/agents-md-maintenance

# Create a PR
gh pr create --title "Add AGENTS.md maintenance workflow" --body "Automated workflow to keep AGENTS.md documentation current with repository changes"
```

**Step 4: Review and merge**

1. Review the PR on GitHub
2. Merge to main

```bash
git checkout main
git pull
```

### Test the Workflow (2 min)

**Step 5: Trigger and observe**

1. Go to **Actions** tab → **agents-md-maintenance** → **Run workflow**
2. Watch it execute

**Say:**

> "Because AGENTS.md is a protected file with `fallback-to-issue`, the agent can't directly create a PR that modifies it. Instead, it falls back to creating an issue with the proposed changes. This ensures a human always reviews changes to critical documentation."

**Point out:**

- The issue created with proposed AGENTS.md updates
- How the workflow documented your recent CI Coach, CI Doctor, and test updater additions
- The `fallback-to-issue` pattern in action

**Key Insight:**

> "The best automation is automation you actually create. By putting the agent directly in your development environment, you remove friction. When it's easy to automate, you automate more."

**Checkpoint:** "Everyone should have the AGENTS.md workflow merged. Let's continue."

---

## Section 8: Exercise 6 - Issue Triage (1:40-1:50) [10 min]

### Learning Objectives

- Reuse proven community workflows with `gh aw add`
- Install and test a battle-tested workflow from githubnext/agentics
- Understand the value of standing on others' shoulders

### Introduction (2 min)

**Say:**

> "You've built several workflows from scratch and from your IDE, which is essential for learning. But in real practice, why reinvent the wheel? The community has built and battle-tested workflows for common needs.
>
> Key sources include:
> - **githubnext/agentics** — Curated, production-ready workflows
> - **github/gh-aw** — Official examples and patterns
> - **github/awesome-copilot** — Community contributions
>
> Let's install a proven issue triage workflow instead of building one from scratch."

### Install Issue Triage (5 min)

**Step 1: Create a branch**

```bash
git checkout main
git pull
git checkout -b workflow/add-issue-triage
```

**Step 2: Add the workflow from the community**

```bash
# Add the workflow from githubnext/agentics
gh aw add githubnext/agentics/issue-triage
```

**Say:**

> "This downloads the workflow and compiles it automatically. No need to write the prompt yourself—this workflow has been refined through real-world usage across many repositories."

**Step 3: Review what was added**

```bash
cat .github/workflows/issue-triage.md
```

**Point out:**

- The 8-step triage process defined in the workflow
- Automatic labeling, duplicate detection, spam filtering
- Structured comments starting with "🎯 Agentic Issue Triage"
- Collapsed sections to keep comments tidy

**Step 4: Commit and create PR**

```bash
git add .
git commit -m "Add issue-triage workflow from githubnext/agentics"
git push -u origin workflow/add-issue-triage
gh pr create --title "Add Issue Triage workflow" --body "Installing the community-proven issue-triage workflow"
```

1. Review and merge the PR
2. Return to main:

```bash
git checkout main
git pull
```

### Test with a New Issue (3 min)

**Step 5: Create a test issue**

**Screen Share:** GitHub Issues → New Issue

**Title:** `Add Ruby adventure support`

**Body:**
```
Currently we have the Python, C# and Javascript. Add a new Ruby adventure to it following the same guidelines as the other languages
```

**Say:**

> "Watch for the 👀 eye emoji icons appearing on the issue—this indicates the workflow is processing it. Go to the Actions tab to see the issue-triage workflow run."

**Step 6: Review the triage output**

**Point out:**

- Labels automatically applied (likely `enhancement` or `feature`)
- The **🎯 Agentic Issue Triage** comment
- How it identifies the issue type and provides helpful context
- Suggested next steps and breakdowns

**Key Insight:**

> "Reusing proven workflows means you get battle-tested solutions immediately. The githubnext/agentics library contains workflows refined through real-world usage. We'll use this Ruby issue in the next exercise."

**Checkpoint:** "Everyone should see the triage comment on their issue. Let's continue."

---

## Section 9: Exercise 7 - Feature Planning (1:50-2:00) [10 min]

### Learning Objectives

- Install the `/plan` command workflow from the community
- See AI break down a feature request into actionable sub-issues
- Understand the full automation cycle: triage → plan → implement

### Introduction (2 min)

**Say:**

> "In Exercise 6, issue-triage gave us a first analysis of the Ruby adventure request. But a high-level feature request like 'Add Ruby support' is too large for a single implementation. Breaking it down manually is tedious and error-prone.
>
> The `/plan` command workflow can analyze any issue and break it into a sequence of clear, actionable sub-issues—perfectly sized for implementation."

### Install Plan Workflow (4 min)

**Step 1: Create a branch and add the workflow**

```bash
git checkout main
git pull
git checkout -b workflow/add-plan
gh aw add githubnext/agentics/plan
```

**Step 2: Commit and create PR**

```bash
git add .
git commit -m "Add plan workflow from githubnext/agentics"
git push -u origin workflow/add-plan
gh pr create --title "Add Plan workflow" --body "Installing the community-proven plan workflow to break down features into actionable sub-issues"
```

1. Review and merge the PR
2. Return to main:

```bash
git checkout main
git pull
```

### Test /plan on the Ruby Issue (4 min)

**Step 3: Trigger the plan workflow**

**Navigate to the Ruby issue from Exercise 6**

**Add a new comment:**

```
/plan
```

**Say:**

> "The `/plan` command triggers a workflow that uses AI to break down this feature into actionable tasks. Important: must be a new comment, and just `/plan`—don't assign to Copilot (that does something different)."

**Step 4: Watch the workflow run**

**Go to Actions tab → Plan Command workflow**

**While waiting:**

> "The AI is analyzing the issue, determining scope, identifying logical work items, and creating sub-issues with objectives, context, approach, files to modify, and acceptance criteria."

**Step 5: Review the generated sub-issues**

**Navigate back to the Ruby issue**

**Point out:**

- Sub-issues created with structured format
- Proper sequencing: Foundation → Implementation → Validation
- Each task sized for a single PR
- Acceptance criteria for verification

**Expected sub-issues might include:**

- Set up Ruby project structure and dependencies
- Implement Ruby solution for Adventure 1
- Implement Ruby solution for Adventure 2
- Add Ruby-specific README and setup instructions
- Add Ruby to CI/CD pipeline for validation

**Step 6 (optional): Mention assigning to Copilot**

**Say:**

> "Now that you have well-structured sub-issues, you can assign them to Copilot for automatic implementation. Open a sub-issue and comment `assign: copilot`. Copilot reads the specification, creates a branch, writes the code, and opens a PR. That closes the full automation loop: triage → plan → implement → review."

**Key Insight:**

> "The `/plan` command transforms vague feature requests into executable work packages. Each sub-issue is ready for implementation, properly sequenced, and sized for a single PR."

**Checkpoint:** "Can everyone see their sub-issues? We're now at the end of guided exercises."

---

## Section 10: Wrap-up & Q&A (2:00-2:15) [15 min]

### Exercise 8: Explore on Your Own (5 min)

**Say:**

> "You now have all the skills to create, install, and manage agentic workflows. Use the next few minutes to try one of these challenges—or come up with your own. There are no step-by-step instructions this time."

**Show the challenges on screen:**

- **Challenge A: Keep workflows up to date** — Build a workflow that checks `source:` references in compiled workflows against latest versions (like Dependabot for agentic workflows)
- **Challenge B: Re-run your daily report** — Trigger it again and compare to your first run. With all the PRs, issues, and workflows you've added, it should be much more interesting now.
- **Challenge C: Browse community workflows** — Explore githubnext/agentics and install something that catches your eye with `gh aw add`
- **Challenge D: Assign a sub-issue to Copilot** — Open a sub-issue from Exercise 7 and comment `@copilot implement this` to close the full automation loop
- **Challenge E: Build your own** — Create a workflow from scratch that solves a real problem

**Say:**

> "Pick whatever interests you. While you explore, I'll start the retrospective. Feel free to keep working while we discuss."

### Retrospective (3 min)

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

2. **Multiple Approaches, Choose the Right One**
   - Interactive CLI: Learning and simple tasks
   - Manual creation: Full control and understanding
   - Cloud agent: Production quality with documentation reference
   - Repository agent: Context-aware excellence in your IDE
   - Community workflows (`gh aw add`): Battle-tested solutions

3. **Automation Requires Automation Management**
   - As workflows grow, add orchestration
   - Self-organizing systems emerge naturally
   - Meta-workflows maintain the system

4. **Human-in-the-Loop is Key**
   - AI proposes, humans decide
   - Approval gates for critical operations
   - Protected files with fallback-to-issue pattern
   - Review all auto-generated PRs

5. **Natural Language is Powerful**
   - Describe what you want, not how to do it
   - Reference documentation URLs for better results
   - The quality of the prompt determines the quality of the output
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

**Issue: Cloud agent shows red banner about billing**

- **Cause:** First-time usage, billing not configured for cloud resources
- **Fix:** Profile icon → Settings → Copilot → Features → Billing → Select billing entity (organization)

**Issue: Participant can't create/clone repository**

- **Cause:** Network/firewall restrictions
- **Fix:** Use GitHub Codespaces as alternative environment

**Issue: PRs created by agent don't trigger CI**

- **Cause:** Missing classic token with `repo` and `workflow` scopes
- **Fix:** Create classic PAT and store as `GH_AW_CI_TRIGGER_TOKEN` secret

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

**Version:** 2.0  
**Last Updated:** April 12, 2026  
**Facilitator:** [Your Name]  
**Event:** GitHub Copilot Dev Days 2026
