# Exercise 1: Daily Standup Status

> 📖 **Navigation:** [← Setup Guide](participant-handout-setup.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 2 →](participant-handout-exercise2.md)

---

## Introduction: Why Agentic Workflows?

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

## Exercise 1: Daily Standup Status

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

The command creates **four files**:

1. **`daily-report.md`** - The editable source workflow in `.github/workflows/`
2. **`daily-report.lock.yml`** - The compiled GitHub Actions workflow in `.github/workflows/`
3. **`.gitattributes`** - Git configuration file in the repository root
4. **`.github/aw/actions-lock.json`** - GitHub Actions version lock file

**Understanding the files:**

**`daily-report.md`** contains:
- **Frontmatter** (YAML between `---` markers): Configuration defining triggers, permissions, and tools
- **Natural language instructions**: Your description in markdown format

**`daily-report.lock.yml`** is the compiled workflow that:
- Contains a simplified version of your prompt
- Is what GitHub Actions actually executes
- Gets regenerated when you change the `.md` file

**`.gitattributes`** contains:
```
.github/workflows/*.lock.yml linguist-generated=true merge=ours
```
This configuration:
- Marks all `.lock.yml` files as generated (excluded from language statistics)
- Sets merge strategy to `ours` (automatically resolves merge conflicts by keeping your version)

**`.github/aw/actions-lock.json`** locks GitHub Actions to specific versions and commit SHAs:
```json
{
  "entries": {
    "actions/checkout@v6.0.2": {
      "repo": "actions/checkout",
      "version": "v6.0.2",
      "sha": "de0fac2e4500dabe0009e67214ff5f5447ce83dd"
    },
    ...
  }
}
```
This file is a cache of resolved `action@version` → commit SHA mappings. During workflow compilation, the compiler tries to pin each action reference to an immutable commit SHA for security. The cache avoids problems when compiling with limited-permission tokens (like GitHub Copilot Coding Agent) that may not have access to resolve external repositories. Without this cache, compilation can be unstable—succeeding with a permissive token but failing when token access is restricted. Commit this file to version control so all contributors use consistent action references.

📚 **Learn more:** [What is the actions-lock.json file?](https://github.github.com/gh-aw/reference/faq/#what-is-the-actions-lockjson-file)

📚 **Learn more:** [How Agentic Workflows Work](https://github.github.com/gh-aw/introduction/how-they-work/)

**Step 3: Observe the limitation**

Open `.github/workflows/daily-report.md` and look at the prompt. It's very basic - just your description. This works, but we can achieve much better results.

**Why this matters:** The quality of the AI's output depends heavily on the quality and detail of the instructions. The simple interactive CLI creates a minimal prompt, which means the workflow might:
- Miss important details
- Not format output consistently
- Lack error handling
- Be less reliable

**What's next:** In the following exercises, we'll use more sophisticated approaches that generate better prompts and higher-quality workflows.

**Step 4: Commit and test**

```bash
# Review the generated files or view in your code editor
cat .github/workflows/daily-report.md
cat .github/workflows/daily-report.lock.yml

# Commit all files
git add .
git commit -m "Add daily report workflow (basic version)"
git push
```

**Step 5: Manually trigger to test**

Since it's scheduled for daily execution, trigger it manually to see it work:

1. Go to your repository on GitHub
2. Click **Actions** tab
3. Select **daily-report** workflow
4. Click **Run workflow** button
5. Watch it execute

![Workflow execution progress](images/workflow-progress.png)

**Understanding the workflow execution:**

The workflow runs through **5 distinct phases**:

1. **activation** (✅ ~16s) - Sets up the workflow environment, checks out the repository code, and prepares the runtime
2. **agent** (✅ ~2m) - The AI agent analyzes your repository, reads commits, PRs, and issues from the past 24 hours, and formulates a summary
3. **detection** (🟡 ~45s) - Validates the agent's output to ensure it's properly formatted and safe to process
4. **safe_outputs** (⚪ pending) - **This is the automation step** that interprets the JSON output from the agent and creates the actual issue in your repository
5. **conclusion** (⚪ pending) - Finalizes the workflow and cleans up

**Important:** The agent itself doesn't directly create issues, PRs, or comments. Instead, it produces **structured JSON output** that describes what should be created. The `safe_outputs` step then interprets this JSON and performs the actual GitHub API calls to create the issue. This separation ensures security and allows for validation before any changes are made to your repository.

---

## Exercise 1b: Upgrade Daily Report with Cloud Agent

**Why: From Basic to Production-Quality**

In Exercise 1, you used the interactive CLI to create a daily-report workflow. It works, but the prompt is minimal—just your one-line description. The cloud agent produces significantly better workflows because it can **download and reference the official documentation** while generating the workflow. This means richer prompts, better error handling, and more consistent output formatting.

Think of it this way: the CLI is like writing a quick note from memory, while the cloud agent is like writing with the documentation open in front of you.

**What: A Smarter Daily Report**

By updating the existing workflow through the cloud agent, you'll get:
- **Detailed, structured prompts** generated from documentation best practices
- **Better formatting** for the daily summary issue
- **More comprehensive coverage** of repository activity
- **A Pull Request** with the changes, so you can compare before and after

**How: Update Using the Cloud Agent**

**Method:** We'll use the cloud agent (web browser) to upgrade the existing daily-report workflow.

**Step 1: Navigate to the cloud agent**

1. Go to your repository on GitHub.com in your web browser
2. Click on the **Agent** tab (next to Code, Issues, Pull Requests, etc.)

**⚠️ First-time setup — Configure billing for cloud resources:**

If this is your first time using the cloud agent, you may see a **red banner** instructing you to configure billing for cloud resources and premium requests. To resolve this:

1. Click the link in the banner, or navigate manually:
   - Click your **profile icon** (top-right) → **Settings**
   - In the left sidebar: **Copilot** → **Features**
2. Scroll down to the **Billing** section
3. Under **"Usage billed to"**, click **"Select billing entity"**
4. Select the **organization** where you receive your Copilot license from

![Copilot billing configuration](images/usage-billing.png)

Once configured, return to your repository and click the **Agent** tab again.

**Step 2: Provide the upgrade prompt**

In the cloud agent chat, provide this prompt:

```
Update the existing daily-report workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md. Create a Pull Request when you're done.

The purpose of the workflow is to act as a daily report that helps team members keep up to date. It should:
Run daily at 9 AM and create an issue with a summary of repository activity from past 24 hours. Include commits, pull requests, issues, and CI/CD failures.

Use the schedule trigger and create issues using safe-outputs.
```

**Step 3: Review and merge the generated PR**

The cloud agent creates a **Pull Request** with the updated workflow files.

1. Go to your repository on GitHub → **Pull Requests** tab
2. Review the PR created by the agent
3. **Compare the changes:** Look at how the cloud agent improved the prompt in `.github/workflows/daily-report.md` compared to the basic version from Exercise 1
4. Verify the workflow files:
   - `.github/workflows/daily-report.md` (updated source workflow)
   - `.github/workflows/daily-report.lock.yml` (recompiled workflow)
5. **Merge the PR to main**

**Step 4: Pull the changes locally**

```bash
git pull
```

**Step 5: Compare the improvement**

Open `.github/workflows/daily-report.md` and notice how much richer the prompt is now. The cloud agent typically adds:
- Structured output formatting instructions
- Specific sections for commits, PRs, issues, and failures
- Error handling guidance
- Tone and style direction

**Step 6: Trigger the upgraded workflow**

Now let's run the improved version and compare the output:

1. Go to your repository → **Actions** tab
2. Select **daily-report** workflow
3. Click **Run workflow** button → Run workflow
4. Watch it execute through the same 5 phases (activation → agent → detection → safe_outputs → conclusion)

The resulting issue should contain roughly the same information as before, but now the output is **better structured and formatted**. The cloud agent's richer prompt gives the AI clearer instructions on how to organize commits, PRs, issues, and failures—so the generated issue is more consistent and easier to read during standups.

**Key Insight:** The same workflow purpose, but dramatically better instructions. This is why we use the cloud agent for all subsequent exercises—it consistently produces higher-quality workflows by referencing the official documentation during generation.

---

> 📖 **Navigation:** [← Setup Guide](participant-handout-setup.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 2 →](participant-handout-exercise2.md)
