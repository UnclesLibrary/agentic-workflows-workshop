# Exercise 5: Create Workflow with Repository Agent

> 📖 **Navigation:** [← Exercise 4](participant-handout-exercise4.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 6 →](participant-handout-exercise6.md)

---

**Why: Bringing Automation into Your IDE**

So far, you've created workflows using:
- **Interactive CLI** (Exercise 1) - Quick, but produces minimal prompts
- **Manual creation** (Exercises 2-3) - Full control, but requires knowing the workflow format
- **Cloud Agent** (Exercises 1b, 4) - Good quality, but requires switching to the browser

**The challenge:** Most developers spend their time in their IDE (like VS Code), not on GitHub.com. Every time you switch to the browser to create a workflow, you lose focus and momentum.

**What: Repository Agent in VS Code**

Remember the `gh aw init` you ran in Exercise 2? That configured the MCP server and repository agent. Now you can use **GitHub Copilot Chat directly in VS Code** to create agentic workflows — no browser needed.

This means:
- **Stay in your IDE** - No context switching
- **Faster workflow creation** - Agent is right where you're coding
- **Immediate testing** - Generate, compile, commit, and test without leaving VS Code
- **Full repository context** - The agent understands your codebase

**How: Create a Workflow from VS Code**

**Step 1: Create a branch**

```bash
git checkout main
git pull
git checkout -b workflow/agents-md-maintenance
```

**Step 2: Use the repository agent in VS Code**

1. **Open VS Code Copilot Chat**
2. Type `/agents` to view available agents
3. Select the **agentic-workflows** agent from the UI
4. Provide this prompt:

```
create a workflow that keeps the AGENTS.md file up to date.

It should run weekly, review merged pull requests and updated source files since the last run, then open a pull request that keeps AGENTS.md accurate and current.

make sure to allow the agents.md file, as it is an a protected file
---
    allowed-files: ["AGENTS.md"]
    protected-files: fallback-to-issue
---

```

When copilot asks to get some web reference choose allow. Same goes if it wants to compile the workflow.

5. The agent generates the workflow right in VS Code with full repository context

**Step 3: Compile, commit, and create PR**

Notice how seamless this is - you stayed in your IDE the entire time:

```bash
# Save the generated workflow file (e.g., .github/workflows/agents-md-maintenance.md)
# The agent will have created the .md file with your workflow

# Compile the workflow to create the lock file
gh aw compile agents-md-maintenance

# This creates .github/workflows/agents-md-maintenance.lock.yml

# Add both files
git add .

# Commit with a clear message
git commit -m "Add AGENTS.md maintenance workflow"

# Push the branch
git push -u origin workflow/agents-md-maintenance

# Create a PR
gh pr create --title "Add AGENTS.md maintenance workflow" --body "Automated workflow to keep AGENTS.md documentation current with repository changes"
```

**Step 4: Review and merge the PR**

1. Go to your repository → **Pull Requests** tab
2. Review the PR with the new workflow
3. **Merge the PR to main**
4. Return to your local main branch:

```bash
git checkout main
git pull origin main
```

**Step 5: Test the AGENTS.md updater**

Now let's see the workflow in action. It should analyze all the recent PRs you've merged (CI Coach, CI Doctor, Test Updater, and the initialization) and update AGENTS.md accordingly.

1. Go to your repository → **Actions** tab
2. Select the **agents-md-maintenance** workflow (or similar name)
3. Click **Run workflow** button → Run workflow
4. Watch it execute

The workflow will:
- Review merged pull requests since the last run
- Analyze the workflows you've added (daily-report, ci-coach, ci-doctor, continuous-test-updates)
- Update AGENTS.md with descriptions of these new workflows

Because `AGENTS.md` is a **protected file** (we configured `protected-files: fallback-to-issue` in the workflow), the agent **cannot directly create a PR** that modifies it. Instead, it falls back to creating an **issue** with the proposed changes.

**Step 6: Review the generated issue and create the PR**

After the workflow completes:
1. Check your repository's **Issues** tab for a new issue created by the workflow
2. The issue will contain the proposed AGENTS.md updates — a summary of the workflows you've added and how the file should be updated
3. At the bottom of the issue, click the **link to create a PR** from the issue content

   ![Create PR from issue](images/pr-from-issue.png)

4. Review the PR with the proposed AGENTS.md changes
5. Notice how the workflow documented your recent changes — it understands the purpose and context of each workflow you added
6. **Merge the PR** to update AGENTS.md

> **💡 Why protected files matter:** This is the `fallback-to-issue` pattern in action. By marking `AGENTS.md` as a protected file, you ensure a human always reviews changes to critical documentation before they're merged. The workflow does the analysis work; you make the final call.

**Key Insight:** The best automation is automation you actually create. By putting the agent directly in your development environment, you remove friction from the workflow creation process. When it's easy to automate, you automate more. This makes the repository agent the most practical method for ongoing workflow development.

---

---

> 📖 **Navigation:** [← Exercise 4](participant-handout-exercise4.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 6 →](participant-handout-exercise6.md)
