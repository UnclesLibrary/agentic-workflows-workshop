# Exercise 8: Explore on Your Own

> 📖 **Navigation:** [← Exercise 7](participant-handout-exercise7.md) | [Back to Overview](participant-handout.md) | [Next: Commands & Resources →](participant-handout-resources.md)

---

You now have all the skills to create, install, and manage agentic workflows. Use the remaining time to try one (or more!) of the following challenges. Pick whatever interests you — there are no step-by-step instructions this time.

---

**🔄 Challenge A: Keep Your Workflows Up to Date**

Your installed workflows have a `source:` reference in their frontmatter that pins them to a specific commit. Open one of your compiled workflows and look for it:

```yaml
source: githubnext/agentics/workflows/issue-triage.md@b0e9cfd3a20372ce7fe0462bb7bbca2272df4a88
```

This is like a dependency version — it can go stale. Build a workflow (or use the repository agent) that:
- Runs weekly
- Checks each workflow's `source:` reference against the latest version in the remote repository
- Opens a PR to update outdated workflows

Think of it as **Dependabot for your agentic workflows**. Hints: you can use `gh aw add` to re-install a workflow and it will update to the latest version. Diff the before/after to generate a changelog.

---

**📊 Challenge B: Re-run Your Daily Report**

Remember Exercise 1? Your daily-report workflow has been quietly collecting data. Trigger it again now:

1. Go to **Actions** → **daily-report** → **Run workflow**
2. Compare this report to the first one you generated

With all the PRs you've merged, issues you've created, and workflows you've added, the report should be **much more interesting** now. It demonstrates how visibility workflows become more valuable over time as repository activity grows.

---

**📦 Challenge C: Browse and Install Community Workflows**

Explore the community workflow libraries and install something that catches your eye:

- **https://github.com/githubnext/agentics/** — Curated, production-ready workflows
- **https://github.com/github/awesome-copilot** — Community contributions

```bash
# Browse what's available
# Pick a workflow and install it
gh aw add githubnext/agentics/<workflow-name>
```

Some ideas: `continuous-documentation-updates`, `stale-bot`, or any workflow that solves a problem you've seen on your own projects.

---

**🤖 Challenge D: Assign a Sub-Issue to Copilot**

In Exercise 7, the `/plan` command created sub-issues for the Ruby adventure. Pick one and let Copilot implement it:

1. Open a sub-issue on GitHub
2. Comment: `@copilot implement this`
3. Watch Copilot create a branch, write code, and open a PR

This closes the full automation loop: **triage → plan → implement → review**.

---

**🛠️ Challenge E: Build Your Own Workflow from Scratch**

Use any method (CLI, cloud agent, repository agent, or manual) to create a workflow that solves a real problem you've encountered. Some inspiration:

- A `/implement` command that reads an issue and creates a draft PR with an implementation
- A workflow that checks for stale branches and opens cleanup PRs
- A weekly summary of open issues grouped by label and priority
- A workflow that enforces PR conventions (title format, description template, required labels)

---

> **💡 Tip:** Whatever you build, remember the patterns from the workshop:
> - Start with `safe-outputs` to keep human review in the loop
> - Use `protected-files: fallback-to-issue` for critical files
> - Test on your workshop repository before bringing it to production
> - Check the community libraries first — someone may have already built it

---

---

> 📖 **Navigation:** [← Exercise 7](participant-handout-exercise7.md) | [Back to Overview](participant-handout.md) | [Next: Commands & Resources →](participant-handout-resources.md)
