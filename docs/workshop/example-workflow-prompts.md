# Example Workflow Prompts Library

## GitHub Agentic Workflows Workshop

This document contains tested workflow prompts you can use in your repositories. Each prompt is designed to work with the different creation methods (interactive CLI, cloud agent, or repository agent).

---

## 📊 Daily Operations & Insights

### 1. Daily Standup Summary

**Use with:** Cloud Agent or Repository Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose of the workflow is to generate a daily standup summary. It should run every weekday morning at 9 AM and create a new issue with:

1. Commits merged since yesterday (grouped by author)
2. Pull requests opened, reviewed, or merged
3. Issues created, updated, or closed
4. CI/CD workflow runs (successful, failed, or in progress)
5. Dependencies that need updating
6. Stale PRs or issues needing attention

Title the issue: "Daily Standup - [date]"
Label it: "daily-standup", "automation"

Format the content to be scannable and actionable for team standups.
```

---

### 2. Weekly Repository Health Report

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs every Monday at 9 AM and generates a comprehensive repository health report as a new discussion post.

The report should include:
- Code metrics: lines added/removed, file changes
- Contributor activity and new contributors
- Pull request statistics (open, merged, average time to merge)
- Issue burndown (created vs closed)
- Test coverage trends
- CI/CD reliability (pass/fail rates)
- Security vulnerabilities or alerts
- Technical debt indicators
- Suggestions for improvements

Post to Discussions in the "Status Updates" category with title: "Weekly Health Report - [date]"
```

---

### 3. Sprint Retrospective Data

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow should run when an issue labeled "sprint-retrospective" is created. It should:

1. Analyze the sprint timeframe (default: last 2 weeks, or use dates in issue body)
2. Gather data about:
   - Velocity (story points completed if tracked in issues)
   - Cycle time (issue creation to close)
   - Code review time
   - Bug vs feature ratio
   - Blockers mentioned in issue comments
   - Celebration-worthy wins
3. Comment on the retrospective issue with structured data
4. Generate visualizations using ASCII charts or tables
5. Suggest discussion topics based on the data

Be objective and helpful in presenting insights.
```

---

## 🧪 Continuous Improvement

### 4. Continuous Test Coverage

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose is to continuously improve test coverage. Run daily and:

1. Analyze code files to find those with <70% test coverage or no tests
2. Prioritize files by:
   - Business logic importance
   - Recent changes
   - Complexity
3. Generate unit tests for the top 3 files
4. Ensure tests:
   - Follow existing test conventions
   - Cover edge cases
   - Are idiomatic for the language
   - Include meaningful descriptions
5. Create a PR with new tests
6. In PR description, explain what's being tested and why

Limit to 3 files per day to keep PRs reviewable.
Work with C#, JavaScript, Python, TypeScript, Java, and Go.
```

---

### 5. Code Quality Refactoring

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs twice weekly (Tuesday and Thursday) to improve code quality through refactoring.

Each run should:
1. Scan the codebase for code quality issues:
   - Functions longer than 50 lines
   - Duplicate code blocks
   - Complex nested conditionals
   - Magic numbers
   - Poor variable names
   - Missing error handling
2. Select 2-3 issues to fix
3. Apply refactorings while preserving behavior
4. Ensure all tests still pass
5. Create a PR with:
   - Clear explanation of what was refactored
   - Why the refactoring improves code quality
   - Before/after comparisons
   - Test results
6. Label PR: "refactoring", "code-quality", "auto-generated"

Focus on incremental improvements, not large rewrites.
```

---

### 6. Documentation Synchronization

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow keeps documentation synchronized with code. Run daily and:

1. Identify code changes in the last 24 hours
2. Check if documentation files need updates:
   - README.md if setup/usage changed
   - API documentation if public interfaces changed
   - Architecture docs if structure changed
   - Contributing guide if process changed
   - Inline code comments if logic changed
3. Generate documentation updates that:
   - Match the existing documentation style
   - Include code examples
   - Update version numbers or dates
   - Fix broken links
   - Add or update diagrams (as ASCII or Mermaid)
4. Create a PR with all documentation updates
5. Request review from code change authors

Label PRs: "documentation", "auto-sync"
```

---

### 7. Dependency Security Auditor

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs weekly on Monday mornings to audit dependencies for security issues and maintainability.

The workflow should:
1. Scan all dependency files (package.json, requirements.txt, *.csproj, go.mod, etc.)
2. Check for:
   - Known security vulnerabilities
   - Deprecated packages
   - Outdated versions (more than 6 months old)
   - Abandoned packages (no updates in 2+ years)
   - License compliance issues
3. Prioritize by severity and risk
4. Create an issue with findings:
   - Executive summary
   - Critical vulnerabilities (action needed now)
   - Maintenance updates (plan for sprint)
   - Long-term concerns
   - Recommended update order
5. If safe updates identified, create a PR with:
   - Update to patch versions
   - Run tests to verify
   - Include changelog links

Label issues: "dependencies", "security"
```

---

## 🤖 CI/CD Enhancement

### 8. CI Coach - Proactive PR Analysis

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

Act as a CI Coach that runs when pull requests are opened or updated. The workflow should:

1. Analyze the PR changes before CI runs
2. Look for potential issues:
   - Missing tests for new code
   - Breaking changes in public APIs
   - Large file additions
   - Dependency additions without security review
   - Code patterns known to cause CI failures
   - Missing documentation updates
   - Linting issues
   - Database migration concerns
3. Comment on the PR with:
   - Proactive suggestions
   - Estimated CI run time
   - Potential blockers
   - Encouragement and helpful tips
4. Use a friendly, coaching tone
5. Update the comment if new commits are pushed

Be helpful, not critical. Focus on preventing issues before CI runs.
```

---

### 9. CI Doctor - Failure Diagnostics

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

Act as a CI Doctor that runs when any workflow fails. The workflow should:

1. Immediately analyze the failed workflow:
   - Parse error logs
   - Identify root cause (dependencies, tests, linting, timeouts, etc.)
   - Check if it's a known issue
   - Determine if it's flaky or persistent
2. Search repository history:
   - Similar failures and how they were fixed
   - Recent changes that might have caused this
   - Related issues or PRs
3. Take action based on failure type:
   - If simple fix (dependency, typo): Create a PR to fix it
   - If test flake: Create an issue and add "flaky-test" label
   - If persistent: Create detailed issue with debugging guide
4. Comment on the failed PR (if applicable) with:
   - Root cause analysis
   - Suggested fixes
   - Links to relevant documentation
   - Estimated fix time
5. Send notification to issue/discussion if critical

Be diagnostic and solution-oriented.
```

---

### 10. Performance Regression Detector

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs on every PR to detect performance regressions.

The workflow should:
1. Identify performance-critical code changes (database queries, algorithms, API endpoints)
2. Run performance benchmarks comparing the PR branch to main
3. Analyze results for:
   - Execution time increases (>10% slower)
   - Memory usage increases
   - Database query counts
   - API response times
4. If regressions detected:
   - Comment on PR with performance comparison
   - Add "performance-regression" label
   - Request review from performance team
   - Block merge if regression >25%
5. If improvements detected:
   - Celebrate with positive comment
   - Add "performance-improvement" label

Include graphs or tables showing before/after metrics.
```

---

## 📋 Issue & Project Management

### 11. Intelligent Issue Triage

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow should run when new issues are opened. It should:

1. Analyze the issue content to determine:
   - Type: bug, feature request, question, documentation, enhancement
   - Severity: critical, high, medium, low
   - Complexity: simple, moderate, complex
   - Area: frontend, backend, infrastructure, documentation, etc.
2. Check for duplicates by comparing with existing issues
3. Validate if required information is present:
   - For bugs: steps to reproduce, expected vs actual behavior
   - For features: use case, user story, acceptance criteria
4. Take actions:
   - Add labels based on classification
   - Add to project board in appropriate column
   - Assign to team/person if ownership is clear
   - Link to related issues or documentation
   - If duplicate: comment with link and suggest closing
   - If question: suggest moving to Discussions
   - If missing info: comment with template to fill out
5. Post a welcoming comment with the analysis

Be friendly and help issue creators succeed.
```

---

### 12. Issue Planner with /plan Command

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that triggers when someone comments "/plan" on an issue.

The workflow should:
1. Read the issue description and all comments
2. Analyze the feature/task and break it into:
   - Implementation steps (logical order)
   - Required changes per step
   - Dependencies between steps
   - Testing requirements
   - Documentation needs
3. Estimate effort for each step
4. Identify potential risks or blockers
5. Suggest assignment of tasks to team members (based on past contributions)
6. Comment on the issue with:
   - Detailed implementation plan
   - Checklist format for tracking
   - Optional: create sub-issues for each major step
   - Timeline estimate
7. Add "planned" label

The plan should be actionable and detailed enough for developers to start work immediately.
```

---

### 13. Repository Assistant for Issue Management

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a repository assistant workflow that runs daily to manage and organize issues.

The workflow should:
1. Review all open issues and:
   - Close automation-generated issues older than 7 days (standups, reports)
   - Identify stale issues (no activity in 30 days)
   - Find issues missing labels or assignments
   - Detect issues that should be moved to Discussions
   - Find duplicate or related issues
2. Organize issues:
   - Group by theme/area
   - Prioritize by labels and comments
   - Identify quick wins (simple issues with high impact)
   - Flag issues needing triage
3. Create a "Repository Health Dashboard" issue with:
   - Issue statistics and trends
   - Priority issues needing attention
   - Recommendations for cleanup
   - Celebration of issues closed
   - Suggestions for what to work on next
4. Automate where appropriate:
   - Add "stale" label and friendly reminder comments
   - Close obviously obsolete issues
   - Move questions to discussions

Run daily at midnight UTC. Be respectful of human-created issues.
```

---

### 14. Pull Request Reminder

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow should run daily at 10 AM and handle PR reminders:

1. Find PRs that need attention:
   - Waiting for review (no reviews yet, >24 hours old)
   - Changes requested (>3 days since last review)
   - Approved but not merged (>2 days)
   - Has merge conflicts
   - Has failing CI
2. For each PR:
   - Determine who should be notified (author, reviewers, assignees)
   - Create personalized reminder based on PR state
   - Mention specific blockers
3. Post gentle reminder comments with:
   - Summary of PR state
   - What action is needed
   - Who can help unblock
   - Links to CI logs if failing
4. Create a summary issue: "PRs Needing Attention - [date]"
5. Send to team Discussion or Slack (if integrated)

Use friendly, non-pushy language. We want to help, not nag.
```

---

## 🔧 Maintenance & Operations

### 15. AGENTS.md Maintenance

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs weekly to maintain the AGENTS.md file.

The workflow should:
1. Review activity since last run:
   - Merged pull requests
   - Updated source files
   - New features or changes
   - Modified coding conventions
2. Analyze if AGENTS.md needs updates:
   - Project structure changes
   - New patterns or conventions
   - Updated development workflows
   - New dependencies or tools
   - Changed architecture
3. Generate updates to AGENTS.md that:
   - Reflect current reality
   - Help AI agents understand the project
   - Include examples from actual code
   - Update sections that are out of date
   - Add new sections if needed
4. Create a PR with:
   - Updated AGENTS.md
   - Explanation of what changed and why
   - References to source changes

Keep AGENTS.md accurate so agents can help effectively.
```

---

### 16. Workflow Maintenance from Remote

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose is to automatically maintain workflows imported from other repositories.

Run weekly and:
1. Identify workflows that were imported from external sources (check comments or metadata)
2. For each imported workflow:
   - Fetch the latest version from source repository
   - Compare our version to latest
   - Check if updates are available
3. If updates exist:
   - Analyze changes (diff)
   - Determine if updates are compatible
   - Create a branch
   - Update the workflow file
   - Add comment explaining what changed
   - Run validation tests
4. Create a PR with:
   - All updated workflows
   - Changelog for each
   - Breaking changes highlighted
   - Test results
5. Label PR: "dependencies", "workflows", "auto-update"
6. Request review from team

Keep workflows up to date with best practices from the community.
```

---

### 17. License Compliance Checker

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow ensures license compliance across all dependencies.

Run weekly and when dependencies change:
1. Scan all dependency files for licenses
2. Check each dependency license against approved list
3. Flag concerns:
   - Copyleft licenses (GPL, AGPL) in commercial projects
   - Unknown or missing licenses
   - Recently changed licenses
   - Incompatible license combinations
4. Generate report with:
   - All dependencies and their licenses
   - Compliance status (green/yellow/red)
   - Action items for non-compliant dependencies
   - Alternative suggestions for problematic dependencies
5. Create an issue if problems found:
   - Severity-based on license type
   - Recommendations for resolution
   - Links to license documentation
6. Update LICENSES.md file with current state

Label issues: "legal", "compliance", "dependencies"
```

---

### 18. Dead Code Detector

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs monthly to detect and remove dead code.

The workflow should:
1. Analyze the codebase to find:
   - Unused functions or methods
   - Unreachable code branches
   - Commented-out code blocks (>10 lines)
   - Unused imports or dependencies
   - Obsolete files not referenced anywhere
   - Feature flags for completed rollouts
2. Verify findings:
   - Check if code is used in tests
   - Search for dynamic invocations
   - Look for references in documentation
3. Categorize by confidence:
   - High confidence: definitely unused
   - Medium confidence: likely unused
   - Low confidence: might be used dynamically
4. Create a PR that:
   - Removes high-confidence dead code
   - Adds TODO comments for medium confidence
   - Lists low confidence in PR description
5. Ensure all tests pass after removal

Be conservative. It's better to keep questionable code than break something.
```

---

## 🎓 Learning & Onboarding

### 19. New Contributor Greeter

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow welcomes first-time contributors and helps them succeed.

When someone opens their first PR or issue:
1. Detect it's their first contribution
2. Post a welcoming comment that:
   - Thanks them for contributing
   - Links to CONTRIBUTING.md
   - Explains the review process
   - Sets expectations for response time
   - Offers help if they need it
   - Tags a maintainer for review
3. Check if their PR:
   - Follows contribution guidelines
   - Has tests
   - Has been linted
   - Includes documentation
4. If missing elements:
   - Gently point out what's needed
   - Link to examples of good PRs
   - Offer specific guidance
5. Add "first-contribution" label
6. Add to new contributor tracking

Be extra welcoming and supportive. First impressions matter!
```

---

### 20. Code Review Learning Bot

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that helps team members improve their code review skills.

Run when PRs are reviewed and:
1. Analyze the review comments:
   - What was good about the review
   - What could be improved
   - Tone and helpfulness
   - Specificity and actionability
2. Check if reviews cover:
   - Correctness
   - Tests
   - Documentation
   - Design/architecture
   - Performance
   - Security
3. After PR is merged:
   - Send private feedback to reviewer (via Discussion or issue)
   - Highlight excellent review comments
   - Suggest areas for improvement
   - Link to code review best practices
   - Track reviewer growth over time
4. Monthly: Create a "Code Review Stats" report:
   - Most helpful reviewers
   - Review patterns and trends
   - Team learning progress

Be encouraging. The goal is improvement, not judgment.
```

---

## 🔐 Security & Compliance

### 21. Security Checklist for PRs

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow enforces security checks on all PRs.

Run on PR open/update and:
1. Scan code changes for security concerns:
   - Hard-coded secrets or API keys
   - SQL injection vulnerabilities
   - XSS vulnerabilities
   - Insecure dependencies
   - Exposed sensitive endpoints
   - Missing authentication/authorization
   - Unsafe deserialization
   - Command injection risks
2. Check for security best practices:
   - Input validation
   - Output encoding
   - Using parameterized queries
   - HTTPS for all external calls
   - Proper error handling (no info disclosure)
3. Comment on PR with findings:
   - Critical issues (block merge)
   - Warnings (review required)
   - Suggestions (best practices)
4. Add labels: "security-review-needed" if issues found
5. Request review from security team for critical issues

Be specific about what's wrong and how to fix it.
```

---

### 22. Audit Log Analyzer

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that runs daily to analyze repository audit logs for unusual activity.

The workflow should:
1. Fetch audit log events from the last 24 hours:
   - Permission changes
   - Branch protection modifications
   - Secret access
   - Workflow manual runs
   - Settings changes
   - Team membership changes
2. Analyze for anomalies:
   - Actions by users who rarely contribute
   - After-hours administrative changes
   - Bulk deletions
   - Permission escalations
   - Failed authentication attempts (if available)
3. Score events by risk level
4. Create a daily security digest:
   - Normal activity summary
   - Flagged events for review
   - Recommended actions
5. If high-risk activity:
   - Create immediate alert issue
   - Notify security team
   - Suggest rollback actions if needed

Label issues: "security", "audit", "needs-review"
```

---

## 🌐 Community & Communication

### 23. Discussion Curator

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow helps manage GitHub Discussions effectively.

Run daily and:
1. Review discussions from the last 24 hours:
   - Unanswered questions
   - Popular or trending topics
   - Discussions that became actionable (should be issues)
   - Resolved discussions
2. Take actions:
   - If question answered: mark as answered, thank participants
   - If discussion identified a bug/feature: suggest creating issue
   - If discussion inactive for 30 days: mark as stale
   - If discussion has valuable info: suggest adding to wiki/docs
3. Organize discussions:
   - Suggest recategorization if needed
   - Pin important announcements
   - Lock resolved or archived discussions
4. Create weekly "Discussions Digest":
   - Highlight interesting discussions
   - Summarize key insights
   - Link to new issues created from discussions
   - Celebrate community participation

Foster a welcoming and organized community space.
```

---

### 24. Release Notes Generator

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that generates release notes when a new tag is created.

When a version tag is pushed (v*.*.*), the workflow should:
1. Collect changes since last release:
   - Merged PRs
   - Closed issues
   - Commits
2. Categorize changes:
   - 🚀 Features (new functionality)
   - 🐛 Bug Fixes
   - 📚 Documentation
   - 🔧 Maintenance
   - ⚠️ Breaking Changes
   - 🔒 Security
   - ⚡ Performance
3. Generate release notes with:
   - Highlights section (most important changes)
   - Full changelog by category
   - Contributors list
   - Upgrade instructions if breaking changes
   - Links to PRs and issues
   - Installation instructions
4. Create GitHub Release with:
   - Generated notes
   - Built artifacts (if applicable)
   - Proper version tagging
5. Post announcement to Discussions

Make release notes human-readable and marketing-friendly.
```

---

## 📈 Metrics & Analytics

### 25. Contributor Analytics

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow tracks contributor health and engagement.

Run weekly and:
1. Analyze contributor activity:
   - Commits per contributor
   - PR authorship and reviews
   - Issue participation
   - Discussion engagement
   - New contributors
   - Returning contributors
   - Inactive contributors
2. Calculate metrics:
   - Bus factor (dependency on key contributors)
   - Contributor diversity
   - First-response time for new contributors
   - Contribution retention rate
3. Identify patterns:
   - Contributors at risk of burnout (high activity)
   - Contributors drifting away (decreasing activity)
   - Areas lacking expertise
4. Create report as Discussion post:
   - Contribution trends
   - Celebrate active contributors
   - Suggestions for improving contributor experience
   - Recommended focus areas for recruiting

Be data-driven but human-focused.
```

---

## 🎯 Advanced Patterns

### 26. Multi-Repo Orchestrator

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent, requires setup)

```
create a workflow that orchestrates changes across multiple related repositories.

When an issue is labeled "multi-repo", the workflow should:
1. Analyze the issue to determine which repos are affected
2. Create a tracking issue in each affected repository:
   - Link back to the main issue
   - Describe what needs to change in that repo
   - Assign based on repo ownership
3. Create branches in each repo with consistent naming
4. Coordinate implementations:
   - Track progress across all repos
   - Update main issue with status
   - Detect when all repos are ready
5. When all PRs are approved:
   - Create merge plan (order of merging)
   - Coordinate merging
   - Run integration tests
6. Close main issue when all changes are deployed

Add "orchestration" label. This enables coordinated multi-repo features.
```

---

### 27. Intelligent Rollback System

**Use with:** Repository Agent (use `/agents` and select agentic-workflows agent)

```
create a workflow that intelligently handles rollbacks when issues are detected in production.

When an issue is labeled "production-incident" and "needs-rollback":
1. Analyze the issue:
   - What's broken
   - When it started (correlate with deployments)
   - Identify likely culprit PR/commit
2. Find the safe rollback point:
   - Last known good commit
   - Check if simple revert is possible
   - Identify dependencies
3. Create rollback PR:
   - Revert problematic changes
   - Include detailed explanation
   - Add tests to prevent recurrence
   - Update docs if needed
4. Run full test suite automatically
5. If tests pass:
   - Request expedited review
   - Add "rollback" and "urgent" labels
   - Notify on-call team
6. After merge:
   - Create follow-up issue to fix properly
   - Document the incident
   - Update runbooks

Speed and safety are both critical.
```

---

### 28. Feature Flag Lifecycle Manager

**Use with:** Cloud Agent

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The workflow manages the lifecycle of feature flags.

Run weekly and:
1. Scan codebase for feature flag usage
2. For each feature flag, determine:
   - When it was introduced
   - Current rollout percentage (if available)
   - How widely it's used in code
   - If it's always on/off in production
3. Identify flags ready for cleanup:
   - Rolled out to 100% for >30 days
   - Never enabled (abandoned features)
   - No longer referenced in code
4. Create issues or PRs:
   - To remove obsolete flags
   - To fully roll out stable flags
   - To clean up unused flags
5. Maintain a feature flag registry:
   - All current flags
   - Their status
   - Owners
   - Rollout plans
6. Alert teams about:
   - Flags in limbo (neither on nor off)
   - Very old flags (>6 months)

Keep the codebase clean of technical debt from flags.
```

---

## 📝 Notes for Using These Prompts

### Tips for Best Results

1. **Be Specific**: Add details about your repository structure, languages, and conventions
2. **Reference Docs**: Always include the creation guide URL when using cloud agent
3. **Iterate**: Start with these prompts, then refine based on results
4. **Combine**: Mix and match ideas from multiple prompts
5. **Customize**: Adapt to your team's specific needs and workflow

### Testing Approach

1. Test workflows on a private repository first
2. Run manually before setting up automatic triggers
3. Review generated PRs carefully before merging
4. Adjust prompts based on actual output quality
5. Start with read-only workflows, then add write permissions

### Maintenance

- Review workflow effectiveness monthly
- Update prompts as agentic workflows evolve
- Document what works well for your team
- Share successful workflows with community
- Archive workflows that aren't providing value

---

## 🤝 Contributing Your Prompts

Did you create an amazing workflow? Share it!

1. Fork the repository
2. Add your prompt to this file
3. Include:
   - Clear title and description
   - Which creation method works best
   - Any prerequisites
   - Expected outcomes
4. Submit a PR

---

**Last Updated:** March 4, 2026  
**Workshop:** GitHub Copilot Dev Days - Agentic Workflows  
**Repository:** https://github.com/microsoft/CopilotAdventures
