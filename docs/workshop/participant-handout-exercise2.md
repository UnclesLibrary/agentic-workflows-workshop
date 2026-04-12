# Exercise 2: CI Coach

> 📖 **Navigation:** [← Exercise 1](participant-handout-exercise1.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 3 →](participant-handout-exercise3.md)

---

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

**How: Create Your CI Coach Manually**

**Method:** This time we'll create the workflow file manually. This teaches you the anatomy of an agentic workflow—the frontmatter configuration and the natural language prompt—so you understand exactly what the CLI and cloud agent generate for you.

**Step 1: Initialize Agentic Workflows**

In Exercise 1, you created a workflow using `gh aw new`, which handled everything for you — including initialization. But now that we're creating a workflow manually, we first need to initialize the agentic workflows tooling in the repository. This sets up the `copilot-setup-steps.yml` file that configures the MCP server powering the AI agent during workflow execution.

Without this initialization, the compiled workflow won't have the infrastructure it needs to run the agent and process `safe-outputs` (like creating pull requests).

```bash
gh aw init
```

This creates the `.github/aw/` directory with configuration files. You can review what was created:

```bash
ls -la .github/aw/
```

**Step 2: Create a branch**

```bash
git pull
git checkout -b add-ci-coach
```

**Step 3: Create the workflow file**

Create a new file at `.github/workflows/ci-coach.md` and paste the following content:

{% raw %}
````markdown
---
description: Daily CI optimization coach that analyzes GitHub Actions workflows for efficiency improvements and cost reduction opportunities

on:
  schedule:
    - cron: daily
  workflow_dispatch:

network:
  allowed:
  - defaults
  - dotnet
  - node
  - python
  - rust
  - java

permissions: read-all

tracker-id: ci-coach-daily

tools:
  github:
    toolsets: [default]
    min-integrity: none
  bash: true
  web-fetch:

safe-outputs:
  create-pull-request:
    expires: 2d
    title-prefix: "[ci-coach] "
    allowed-files:
      - .github/workflows/ci.yml
    protected-files: allowed
    github-token: ${{ secrets.GH_AW_CI_TRIGGER_TOKEN }}
    github-token-for-extra-empty-commit: ${{ secrets.GH_AW_CI_TRIGGER_TOKEN }}
timeout-minutes: 30
engine: copilot
---

# CI Optimization Coach

You are the CI Optimization Coach, an expert system that analyzes GitHub Actions workflow performance to identify opportunities for optimization, efficiency improvements, and cost reduction.

## Mission

Analyze CI workflows daily to identify concrete optimization opportunities that can make the test suite more efficient while minimizing costs and runtime.

## Current Context

- **Repository**: ${{ github.repository }}
- **Run Number**: #${{ github.run_number }}

## Analysis Framework

### Phase 1: Discovery (5 minutes)

Identify all GitHub Actions workflows in the repository:

1. **Find workflow files**: List all `.github/workflows/*.yml` and `.github/workflows/*.yaml` files
2. **Identify CI workflows**: Focus on workflows that run tests, builds, or lints
3. **Gather recent runs**: Use GitHub API to fetch the last 50-100 runs for each workflow
4. **Collect metrics**:
   - Average runtime per workflow
   - Success/failure rates
   - Job-level timing data
   - Cache usage patterns
   - Artifact sizes

### Phase 2: Analysis (10 minutes)

Analyze the collected data for optimization opportunities:

1. **Job Parallelization**
   - Are independent jobs running sequentially?
   - Can the critical path be reduced?
   - Are matrix jobs balanced?

2. **Cache Optimization**
   - Are dependencies cached effectively?
   - What's the cache hit rate?
   - Are cache keys optimal?

3. **Test Suite Structure**
   - Is test execution balanced?
   - Are slow tests identified?
   - Can tests run in parallel?

4. **Resource Sizing**
   - Are job timeouts appropriate?
   - Are runner types optimal?
   - Are jobs failing due to timeouts?

5. **Artifact Management**
   - Are artifacts necessary?
   - Are retention periods appropriate?
   - Can artifact sizes be reduced?

6. **Conditional Execution**
   - Can some jobs skip on certain conditions?
   - Are path filters used effectively?
   - Can workflow dispatch reduce unnecessary runs?

### Phase 3: Prioritization (5 minutes)

For each potential optimization, assess:

- **Impact**: How much time/cost savings? (High/Medium/Low)
- **Risk**: What's the risk of breaking something? (Low/Medium/High)
- **Effort**: How hard is it to implement? (Low/Medium/High)

Focus on **high impact + low risk + low-to-medium effort** optimizations.

### Phase 4: Implementation (8 minutes)

If you identify valuable improvements:

1. **Make focused changes** to workflow files:
   - Use the `edit` tool for precise modifications
   - Add inline comments explaining the optimization
   - Keep changes minimal and surgical

2. **Document the changes** thoroughly in the PR description

3. **Create a pull request** with clear rationale

### Phase 5: No Changes Path (2 minutes)

If no significant improvements are found:

1. Note the analysis results
2. Use the `noop` safe output tool to report "CI workflows analyzed - no optimization opportunities found"
3. Exit gracefully

## Optimization Patterns

### Common High-Value Optimizations

1. **Parallel Job Execution**
   ```yaml
   # Before: Sequential
   test:
     needs: [build]
   lint:
     needs: [build]
   
   # After: Parallel
   test:
     needs: [build]
   lint:
     needs: [build]  # Both run in parallel after build
   ```

2. **Matrix Balancing**
   ```yaml
   # Balance test distribution across matrix jobs
   matrix:
     group: [1, 2, 3, 4]  # Evenly distributed
   ```

3. **Path Filtering**
   ```yaml
   on:
     push:
       paths:
         - 'src/**'
         - 'tests/**'
   ```

### Anti-Patterns to Avoid

❌ **NEVER modify test code to hide failures**
- Don't add `|| true` to failing tests
- Don't suppress error output
- Don't skip failing tests without justification

❌ **Don't over-optimize**
- Avoid changes that save <2% of runtime
- Don't sacrifice clarity for minor gains
- Don't add complexity without clear benefit

## Pull Request Template

When creating a PR, use this structure:

````markdown
### Summary

[Brief description of optimization and expected benefit]

### Optimizations

#### 1. [Optimization Name]

**Type**: [Parallelization/Cache/Testing/Resource/Artifact/Conditional]
**Impact**: Estimated [X minutes/Y%] savings per run
**Risk**: Low/Medium/High

**Changes**:
- [Description of specific changes made]

**Rationale**: [Why this improves efficiency]

<details>
<summary><b>Detailed Analysis</b></summary>

[Metrics, before/after comparisons, supporting data]

</details>

### Expected Impact

- **Time Savings**: ~X minutes per run
- **Cost Reduction**: ~$Y per month (estimated based on 50 runs/month)
- **Risk Level**: Low/Medium/High

### Testing Recommendations

- [ ] Review workflow syntax
- [ ] Test on a feature branch first
- [ ] Monitor first few runs after merge
- [ ] Compare runtime before/after

## Quality Standards

- **Evidence-based**: All recommendations based on actual data
- **Minimal changes**: Surgical improvements, not rewrites
- **Low risk**: Prioritize safe optimizations
- **Measurable**: Include metrics to verify improvements
- **Reversible**: Changes should be easy to roll back

## Success Criteria

✅ Analyzed all GitHub Actions workflows
✅ Collected metrics from recent runs
✅ Identified optimization opportunities OR confirmed workflows are well-optimized
✅ If changes proposed: Created PR with clear rationale and expected impact
✅ If no changes: Used noop tool to report analysis complete
✅ Completed analysis in under 30 minutes

Begin your analysis now. Identify CI workflows, analyze their performance, and either propose optimizations through a pull request or report that no improvements are needed.
````
{% endraw %}

**Understanding the workflow structure:**

Take a moment to study what you just pasted. The file has two parts:

1. **Frontmatter** (between the `---` markers) — This is the configuration that tells GitHub Actions *how* to run the workflow:
   - `on:` — Triggers: runs daily on a schedule and can be triggered manually via `workflow_dispatch`
   - `permissions: read-all` — The agent can read everything but can only write through `safe-outputs`
   - `tools:` — What the agent can use: GitHub API, bash, and web-fetch
   - `safe-outputs:` — The agent's output creates a pull request (not direct changes), with a `[ci-coach]` title prefix
   - `engine: copilot` — Uses GitHub Copilot as the AI engine

2. **Natural language prompt** (after the second `---`) — This is what the AI agent actually reads and follows. Notice how detailed and structured it is compared to the basic prompt from Exercise 1. The 5-phase framework, optimization patterns, anti-patterns, and PR template all guide the agent toward consistent, high-quality results.

**Step 4: Compile the workflow**

```bash
gh aw compile ci-coach
```

This generates `.github/workflows/ci-coach.lock.yml` — the compiled GitHub Actions workflow that will actually execute.

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

1. Go to your repository on GitHub → **Pull Requests** tab
2. Review the PR to verify the workflow files look correct:
   - `.github/workflows/ci-coach.md` (the source workflow you created)
   - `.github/workflows/ci-coach.lock.yml` (the compiled workflow)
3. **Approve and merge the PR to main**

**Step 7: Pull main and trigger the workflow**

```bash
git checkout main
git pull
```

1. Go to your repository → **Actions** tab
2. Select **ci-coach** workflow
3. Click **Run workflow** button → Run workflow
4. Watch it execute through the 5 phases (activation → agent → detection → safe_outputs → conclusion)

**Step 8: Check the outcome**

After the workflow completes, check your repository for a new **Pull Request** with the `[ci-coach]` prefix. The CI Coach will have:
- Analyzed your existing GitHub Actions workflows
- Identified optimization opportunities (if any)
- Created a PR with proposed changes and detailed rationale

If no optimizations were found, the workflow exits gracefully via the `noop` path — which is a perfectly valid outcome for a well-configured repository.

**Step 9: Iterate until tests are added to CI**

The CI Coach is designed to suggest improvements incrementally. On the first run it might propose caching, parallelization, or other optimizations — but it may not immediately suggest adding tests. You need tests in your CI pipeline for Exercise 3 (CI Doctor), so keep iterating:

1. **Review and merge** the PR the CI Coach created (if any)
2. **Re-trigger** the ci-coach workflow: Actions → ci-coach → Run workflow
3. **Check the new PR** — does it add test steps (e.g., `npm test`, `dotnet test`, `pytest`) to `ci.yml`?
4. **If not yet:** merge the PR, and re-trigger again. Each run builds on the previous improvements.
5. **Repeat** until the CI Coach proposes adding tests to one or more build jobs.

Once you get a PR that adds test execution to the CI pipeline, **approve and merge it**. After merging, pull the changes:

```bash
git checkout main
git pull
```

Verify that `.github/workflows/ci.yml` now contains test commands by opening the file and checking the job steps.

**Why this matters for Exercise 3:** The CI Doctor diagnoses *failing* CI checks. If your pipeline only builds but never runs tests, there's nothing meaningful for the CI Doctor to diagnose. By letting the CI Coach evolve your pipeline to include tests, you create the conditions where the CI Doctor can demonstrate its value — analyzing test failures, identifying root causes, and posting actionable fixes.

**Key Insight:** By creating this workflow manually, you now understand exactly what the CLI and cloud agent generate behind the scenes. Every agentic workflow is just a markdown file with frontmatter configuration + a natural language prompt. The quality of the prompt directly determines the quality of the agent's output — which is why the detailed 5-phase framework produces better results than a one-line description.

This continuous feedback strengthens your guardrails as you prepare for more autonomous workflows.


---

> 📖 **Navigation:** [← Exercise 1](participant-handout-exercise1.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 3 →](participant-handout-exercise3.md)
