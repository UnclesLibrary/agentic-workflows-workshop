# Exercise 4: Continuous Test Updates

> 📖 **Navigation:** [← Exercise 3](participant-handout-exercise3.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 5 →](participant-handout-exercise5.md)

---

**Why: Building a Strong Test Foundation Over Time**

Every engineering team knows tests are important, but writing comprehensive test coverage is:
- **Time-consuming** - Tests often take longer to write than the code itself
- **Tedious** - Repetition and boilerplate make it feel like busywork
- **Deprioritized** - "We'll add tests later" often means "We'll never add tests"
- **Overwhelming** - The idea of achieving 80%+ coverage feels impossible

**The challenge:** Teams that try to "catch up" on test coverage in one big initiative often fail. Developers spend weeks writing tests instead of features, morale drops, and the initiative stalls. Meanwhile, untested code becomes technical debt that protects against faulty changes.

**What: Gradual, Sustainable Test Growth**

Instead of a massive test-writing initiative, the Continuous Test Updates workflow:
- **Works incrementally** - Just 3 tests per day, every day
- **Creates manageable PRs** - Easy to review, not overwhelming
- **Learns from your patterns** - Follows existing test conventions in your repository
- **Accumulates steadily** - 3 tests/day = ~1,000 tests/year
- **Focuses strategically** - Identifies files with missing or inadequate coverage

This approach transforms test coverage from a daunting task into a sustainable background process. You review and accept (or pivot on) small batches of tests, and over time your foundation becomes solid without disrupting feature work.

**How: Create Your Continuous Test Updater**

**Method:** We'll use the cloud agent for consistent quality.

**Step 1: Create the workflow using the cloud agent**

1. Go to your repository on GitHub.com in your web browser
2. Click on the **Agent** tab
3. Provide this prompt to the agent:

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

The cloud agent creates a PR with the workflow files.

1. Go to your repository → **Pull Requests** tab
2. Review the PR (titled something like "Add Continuous Test Updates workflow")
3. Verify the workflow files:
   - `.github/workflows/continuous-test-updates.md`
   - `.github/workflows/continuous-test-updates.lock.yml`
4. **Merge the PR to main**

**Step 3: Manually trigger the workflow**

Since this runs on a daily schedule, trigger it manually to see it work immediately:

1. Go to your repository → **Actions** tab
2. Select the **continuous-test-updates** workflow (or similar name)
3. Click **Run workflow** button → Run workflow
4. Watch it execute (this may take a few minutes as it analyzes your codebase)

**Step 4: Review the test suggestions**

After the workflow completes, check your repository for:
- A new **pull request** with proposed tests, or
- A new **issue** with test recommendations

The workflow will:
- Identify specific files that need better test coverage
- Generate tests that match your existing test patterns
- Follow naming conventions already in your codebase
- Create meaningful test cases (not just empty scaffolding)

**Example output you might see:**
- New tests for edge cases in existing functions
- Tests for recently added code that lacks coverage
- Validation tests for input handling
- Integration tests for key workflows

**Step 5: Review and iterate**

When reviewing the proposed tests:
- ✅ **Accept** tests that add value and follow good practices
- 🔄 **Request changes** if tests need adjustment
- ❌ **Close** if the tests aren't relevant (the workflow will try different files next time)

**Key Insight:** By generating 3 tests per day, you build robust test coverage without disrupting feature development. Over weeks and months, this creates a strong validation foundation that protects against faulty changes and enables more confident automation. Better tests mean better AI outcomes - the more validation you have, the safer it is to let AI make autonomous changes.

> **⚠️ Note on coding style:** The workflow generates tests based on the existing test patterns in your repository. If your codebase has consistent test conventions, the generated tests will follow that style. However, if you have a legacy repository with mixed testing styles (different frameworks, naming conventions, assertion libraries), the agent may produce inconsistent results — mirroring the inconsistency it finds. In that case, consider:
> - **Refactoring existing tests** to a consistent style before enabling this workflow
> - **Adding strong `AGENTS.md` instructions** that specify exactly how you want tests structured (framework, naming conventions, assertion style, file organization)
>
> Clear guidance in `AGENTS.md` acts as a style guide for the AI — the more specific your instructions, the more consistent the output.

Your DevOps practices now include proactive quality improvement: visibility (Exercise 1), coaching (Exercise 2), diagnosis (Exercise 3), and continuous validation growth (Exercise 4). These workflows compound over time, each making your repository healthier and your team more productive.

---

---

> 📖 **Navigation:** [← Exercise 3](participant-handout-exercise3.md) | [Back to Overview](participant-handout.md) | [Next: Exercise 5 →](participant-handout-exercise5.md)
