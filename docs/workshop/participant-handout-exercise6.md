# Exercise 6: Issue Triage

> 📖 **Navigation:** [← Exercise 5](participant-handout-exercise5.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 7 →](participant-handout-exercise7.md)

---

**Why: Don't Build What Others Have Perfected**

You've built several workflows from scratch (Exercises 1-4) and from your IDE (Exercise 5), which is essential for learning the fundamentals. But in real practice, why reinvent the wheel when proven solutions exist?

**The challenge:** Building workflows from scratch means:
- **Trial and error** - You'll discover edge cases the hard way
- **Missing features** - You might not think of all the capabilities you need
- **Maintenance burden** - You own all the bugs and improvements
- **Reinventing** - Others have solved these problems and worked out the kinks

**The opportunity:** The community has built and battle-tested workflows for common needs. Key sources include:
- [**https://github.com/githubnext/agentics/**](https://github.com/githubnext/agentics/) - Curated, production-ready workflows
- [**https://github.com/github/gh-aw**](https://github.com/github/gh-aw) - Official examples and patterns
- [**https://github.com/github/awesome-copilot**](https://github.com/github/awesome-copilot) - Community contributions

**What: Issue Triage - Intelligent First Responder**

The `issue-triage` workflow from githubnext/agentics is a focused, battle-tested assistant that runs automatically when issues are opened or reopened. It provides intelligent first-response triage:

**Analyzes Issues Thoroughly:**
- Fetches issue content and comments
- Searches for similar issues to detect duplicates
- Reviews other open issues for context
- Identifies spam or bot-generated issues

**Provides Smart Labeling:**
- Selects appropriate labels from your repository's label list
- Identifies issue type (bug, feature request, question, etc.)
- Assigns priority labels (high, medium, low) based on severity
- Marks duplicates of **open** issues only (not closed ones)

**Delivers Actionable Analysis:**
- Adds structured comment starting with "🎯 Agentic Issue Triage"
- Provides brief summary of the issue
- Suggests debugging strategies and reproduction steps
- Links to relevant resources and documentation
- Breaks down complex issues into sub-task checklists
- Uses collapsed sections to keep comments tidy

**Respects Human Input:**
- Doesn't spam or over-communicate
- Only adds labels when clearly applicable
- Exits early for obvious spam without noise

**How: Add the Community Workflow**

**Method:** Use `gh aw add` to install a proven community workflow.

**Step 1: Create a branch for the addition**

```bash
git checkout main
git pull
git checkout -b workflow/add-issue-triage
```

**Step 2: Add the issue-triage workflow**

```bash
# Add the workflow from the githubnext/agentics repository
gh aw add githubnext/agentics/issue-triage

# This downloads issue-triage.md and compiles it to issue-triage.lock.yml
```

**Step 3: Review what was added**

```bash
# Check the workflow file
cat .github/workflows/issue-triage.md

# Note the 8-step triage process defined in the workflow
```

**Step 4: Commit and create PR**

```bash
# Add both the source and compiled workflow
git add .

# Commit with context
git commit -m "Add issue-triage workflow from githubnext/agentics"

# Push the branch
git push -u origin workflow/add-issue-triage

# Create a PR
gh pr create --title "Add Issue Triage workflow" --body "Installing the community-proven issue-triage workflow to automatically analyze, label, and provide helpful context for new issues"
```

**Step 5: Review and merge the PR**

1. Go to your repository → **Pull Requests** tab
2. Review the PR with the issue-triage workflow
3. **Merge the PR to main**
4. Return to your local main branch:

```bash
git checkout main
git pull origin main
```

**Step 6: Test with a new issue**

Let's trigger the issue-triage workflow:

1. **Create a test issue** on your repository:
   - Title: `Add Ruby adventure support`
   - Body: 
     ```
     Currently we have the Python, C# and Javascript. Add a new Ruby adventure to it following the same guidelines as the other languages
     ```

2. **Watch GitHub pick it up:**
   - Notice the 👀 eye emoji icons appear on the issue — this can take 1-2 minutes as the pipeline needs to start up (this indicates the workflow is processing it)
   - Go to **Actions** tab
   - Find the "issue-triage" workflow run
   - Observe how it processes the new issue

**Step 7: Review the triage output**

After the workflow completes (usually ~1-2 minutes):
1. Return to the issue you created
2. Check the labels that were automatically applied (likely `enhancement` or `feature`)
3. Read the **🎯 Agentic Issue Triage** comment:
   - Does it correctly identify this as a feature request?
   - Did it provide helpful context about the repository?
   - Did it suggest next steps or break down the work?
   - Did it reference similar work in the repository?

**Key Insight:** Reusing proven workflows means you get battle-tested solutions immediately, benefit from community improvements, and avoid common pitfalls. The githubnext/agentics library contains workflows refined through real-world usage across many repositories. By standing on the shoulders of giants, you accelerate from "learning the basics" to "running production-quality automation."

---

---

> 📖 **Navigation:** [← Exercise 5](participant-handout-exercise5.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 7 →](participant-handout-exercise7.md)
