# Exercise 7: Feature Planning

> 📖 **Navigation:** [← Exercise 6](participant-handout-exercise6.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 8 →](participant-handout-exercise8.md)

---

**Why: From Big Ideas to Actionable Tasks**

In Exercise 6, issue-triage gave us a first analysis of the Ruby adventure request. But a high-level feature request like "Add Ruby support" is too large for a single implementation. Breaking it down manually is tedious and error-prone.

**The challenge:** Complex features need decomposition:
- **Manual breakdown is time-consuming** - Thinking through all the steps takes mental energy
- **Easy to miss dependencies** - What needs to happen first? What depends on what?
- **Inconsistent granularity** - Some tasks too large, others too small
- **Hard to parallelize** - Unclear what can be done simultaneously

**The opportunity:** The `/plan` command workflow can analyze any issue and break it into a sequence of clear, actionable sub-issues (up to 5) that are perfectly sized for implementation.

**What: Plan - Intelligent Task Breakdown**

The `plan` workflow from githubnext/agentics is a specialized planning assistant that:

**Analyzes the Request:**
- Reads issue title, description, and all comments
- Determines overall scope and complexity
- Identifies logical work items
- Considers dependencies between tasks

**Creates Sub-Issues with Structure:**
- **Objective:** What needs to be done
- **Context:** Why this is needed and how it relates to the parent issue
- **Approach:** Suggested implementation steps
- **Files:** Specific files to create or modify
- **Acceptance Criteria:** Checklist to verify completion

**Follows Best Practices:**
- **Proper sequencing:** Foundation → Implementation → Validation
- **Right granularity:** Each task completable in a single PR
- **SWE agent-ready:** Written with imperative language for clear execution
- **Automatic linking:** Sub-issues reference the parent issue
- **Maximum 5 tasks:** Keeps scope manageable

**Example sub-issue:**
> **Title:** Add user authentication middleware
> 
> **Objective:** Implement JWT-based authentication middleware for API routes.
> 
> **Context:** This is needed to secure API endpoints before implementing user-specific features. Part of issue #123.
> 
> **Files to Modify:**
> - Create: `src/middleware/auth.js`
> - Update: `src/routes/api.js` (to use the middleware)
> - Update: `tests/middleware/auth.test.js` (add tests)
> 
> **Acceptance Criteria:**
> - [ ] Middleware validates JWT tokens
> - [ ] Invalid tokens return 401 status
> - [ ] Tests cover success and error cases

**How: Add the Planning Workflow**

**Method:** Use `gh aw add` to install the community planning workflow.

**Step 1: Create a branch for the addition**

```bash
git checkout main
git pull
git checkout -b workflow/add-plan
```

**Step 2: Add the plan workflow**

```bash
# Add the workflow from the githubnext/agentics repository
gh aw add githubnext/agentics/plan

# This downloads plan.md and compiles it to plan.lock.yml
```

**Step 3: Review what was added**

```bash
# Check the workflow file
cat .github/workflows/plan.md

# Note the planning assistant guidelines and task breakdown process
```

**Step 4: Commit and create PR**

```bash
# Add both the source and compiled workflow
git add .

# Commit with context
git commit -m "Add plan workflow from githubnext/agentics"

# Push the branch
git push -u origin workflow/add-plan

# Create a PR
gh pr create --title "Add Plan workflow" --body "Installing the community-proven plan workflow to break down features into actionable sub-issues"
```

**Step 5: Review and merge the PR**

1. Go to your repository → **Pull Requests** tab
2. Review the PR with the plan workflow
3. **Merge the PR to main**
4. Return to your local main branch:

```bash
git checkout main
git pull origin main
```

**Step 6: Test with the Ruby issue from Exercise 6**

Now let's use the plan workflow on the "Add Ruby adventure support" issue we created in Exercise 6:

1. **Navigate to the Ruby issue:**
   - Go to your repository → **Issues** tab
   - Find the issue titled "Add Ruby adventure support"
   - Open it

2. **Trigger the plan workflow:**
   - Scroll to the bottom (comment section)
   - Add a **new comment** (not an edit of existing comment):
     ```
     /plan
     ```
   - **Important:** Must be a new comment, editing won't trigger the workflow
   - **Important:** Just `/plan` - don't assign to Copilot (that does something different!)

3. **Watch the workflow run:**
   - Go to **Actions** tab
   - Find the "Plan Command" workflow run
   - Observe how it processes the issue

**Step 7: Review the generated sub-issues**

After the workflow completes (usually ~1-2 minutes):

1. **Return to the Ruby issue:**
   - Check for new sub-issues created
   - They should appear in the issue's "Related" or "Linked issues" section

2. **Review each sub-issue:**
   - Notice the structured format: Objective, Context, Approach, Files, Acceptance Criteria
   - Check the sequencing: Does it make logical sense?
   - Verify granularity: Can each be completed in a single PR?

3. **Expected sub-issues might include:**
   - Set up Ruby project structure and dependencies
   - Implement Ruby solution for Adventure 1
   - Implement Ruby solution for Adventure 2
   - Add Ruby-specific README and setup instructions
   - Add Ruby to CI/CD pipeline for validation

**Step 8 (Optional): Assign a sub-issue to Copilot for automatic implementation**

Now that you have well-structured sub-issues, you can let Copilot implement them automatically:

1. **Select one of the generated sub-issues:**
   - Choose a sub-issue that's well-defined and has clear acceptance criteria
   - Start with a simpler task for your first test

2. **Assign to Copilot:**
   - Open the sub-issue on GitHub
   - In the issue comment section, type:
     ```
     assign: copilot
     ```
   - Post the comment

3. **Watch Copilot Cloud work:**
   - Copilot Cloud picks up the assignment automatically
   - It reads the issue's Objective, Context, Approach, and Acceptance Criteria
   - Creates a new branch for the implementation
   - Writes the code based on the specification
   - Runs tests if applicable
   - Opens a PR with the implementation

4. **Review the PR:**
   - Go to **Pull Requests** tab
   - Find the PR created by Copilot
   - Review the implementation against the acceptance criteria
   - Request changes if needed, or merge if it looks good

**Note:** This demonstrates the full workflow automation cycle: issue triage → planning → automatic implementation. Each sub-issue becomes a self-contained work package that Copilot can execute autonomously.

**Key Insight:** The `/plan` command transforms vague feature requests into executable work packages. Each sub-issue is ready for implementation, properly sequenced, and sized for a single PR. This workflow eliminates the manual planning overhead and ensures consistent quality in task breakdown across your team.

---

---

> 📖 **Navigation:** [← Exercise 6](participant-handout-exercise6.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 8 →](participant-handout-exercise8.md)
