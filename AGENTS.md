# AGENTS.md - AI Agent Guidance for Repository Management

## Repository Overview

**Repository Name:** CopilotDevDays-AgenticWorkflows  
**Purpose:** Complete workshop materials for teaching GitHub Agentic Workflows at community events  
**Primary Technology:** Jekyll-based documentation site  
**Target Audience:** Event organizers, workshop facilitators, and participants learning GitHub Agentic Workflows

## Repository Context

This repository contains battle-tested materials for a 2-hour hands-on workshop (with optional 15-minute extended Q&A) titled "From Code to Automation: Mastering GitHub Agentic Workflows". The workshop teaches participants how to:

- Write intelligent automation workflows in natural language
- Implement continuous improvement patterns
- Automate issue management and triage
- Build CI/CD coaching and diagnostics systems
- Create self-organizing, self-improving repositories

## Repository Structure

```
CopilotDevDays-AgenticWorkflows/
├── .github/                     # GitHub configuration
│   └── workflows/               # GitHub Actions workflows
│       └── pages.yml            # Jekyll site deployment
├── .gitignore                   # Git exclusions
├── README.md                    # Main repository documentation
├── CONTRIBUTING.md              # Contribution guidelines
├── LICENSE                      # MIT License
├── AGENTS.md                    # This file - AI agent guidance
└── docs/                        # Jekyll site root
    ├── _config.yml              # Jekyll configuration
    ├── Gemfile                  # Ruby dependencies
    ├── Gemfile.lock             # Ruby dependency versions
    ├── index.md                 # Site homepage
    ├── _site/                   # Generated site (excluded from git)
    └── workshop/                # Workshop materials
        ├── README.md            # Workshop overview
        ├── gh-agentic-workflows-session.md      # Event organizer materials
        ├── facilitator-guide.md                  # Facilitator instructions
        ├── participant-handout.md                # Student reference guide
        ├── example-workflow-prompts.md           # 28 tested workflow prompts
        ├── slide-deck-outline.md                 # Presentation structure
        └── quick-reference-card.md               # One-page cheat sheet
```

## Content Organization Principles

### Content Hierarchy

1. **Event Organizers** need high-level session descriptions and logistics
2. **Facilitators** need detailed minute-by-minute guides and troubleshooting
3. **Participants** need practical references, commands, and exercises

### Document-Specific Roles

| Document                          | Primary Audience | Key Characteristics                                  |
| --------------------------------- | ---------------- | ---------------------------------------------------- |
| `gh-agentic-workflows-session.md` | Event organizers | Marketing copy, session descriptions, prerequisites  |
| `facilitator-guide.md`            | Workshop leaders | Minute-by-minute timeline, teaching tips, live demos |
| `participant-handout.md`          | Attendees        | Setup commands, exercises, troubleshooting           |
| `example-workflow-prompts.md`     | All              | Library of tested workflow patterns                  |
| `quick-reference-card.md`         | Participants     | One-page printable reference                         |
| `slide-deck-outline.md`           | Facilitators     | Presentation structure                               |

## Content Conventions

### Markdown Style

- Use **ATX-style headers** (`#`, `##`, `###`) for all headings
- Include **emoji icons** (🎯, 🚀, 📦, etc.) for visual hierarchy in top-level documents
- Use **code blocks** with language tags (`bash, `yaml, ```markdown)
- Include **badges** in README.md for visual appeal
- Use **relative links** for internal navigation (Jekyll handles these)

### Workshop Timing Format

Always express timing in this format (using 0:00 as start time):

```
0:00-0:15   Introduction
0:15-0:30   Setup
0:30-1:45   Hands-on Exercises
1:45-2:00   Wrap-up
```

**Note:** The core workshop is 2 hours (0:00-2:00). The facilitator guide may include optional extended time for wrap-up and Q&A (up to 2:15 total).

### Command Format

Present commands with clear context:

````markdown
**Create a new workflow:**

```bash
gh workflow create my-workflow
```
````

````

### Workflow Prompt Format

Example workflow prompts should follow this structure:
```markdown
### 🎯 Workflow Name

**Purpose:** Brief description
**Trigger:** When it runs
**Safety Level:** 🟢 Low risk / 🟡 Medium risk / 🔴 High risk

**Prompt:**
````

Natural language prompt here

```

**What it does:**
- Bullet point 1
- Bullet point 2
```

## Jekyll Site Management

### Local Development

**Start the Jekyll server:**

```bash
cd docs
bundle exec jekyll serve --host 0.0.0.0 --livereload
```

**Install dependencies:**

```bash
cd docs
bundle install
```

**Access the site:**

- Local: http://localhost:4000
- With livereload: Changes auto-refresh in browser

### Jekyll Configuration

The site uses the **Cayman theme** with these key settings:

- Relative links enabled for cross-document navigation
- Automatic title extraction from headings
- Optional front matter (YAML headers are optional)
- Markdown processor: kramdown

### Files to Exclude from Git

- `docs/_site/` - Generated site content (always rebuild)
- `docs/.jekyll-cache/` - Jekyll build cache

**Note:** `docs/Gemfile.lock` is currently committed to the repository to ensure consistent Ruby gem versions across environments.

## Common Agent Tasks

### Task: Update Workshop Duration

**When:** User requests timing changes for exercises or sections

**Actions:**

1. Update timing in `docs/workshop/facilitator-guide.md` (minute-by-minute timeline)
2. Update total duration in `README.md` (Quick Start section and Overview)
3. Update duration badge: `![Workshop Duration](https://img.shields.io/badge/Duration-X%20hours-green)`
4. Update timing in `docs/workshop/gh-agentic-workflows-session.md` (session description)
5. Update timing in `docs/workshop/README.md` if affected
6. Verify total adds up correctly (core workshop is 2 hours, optional extended time up to 2:15)

### Task: Add New Workflow Pattern

**When:** User wants to add a new example workflow prompt

**Actions:**

1. Add to `docs/workshop/example-workflow-prompts.md` in the appropriate category
2. Follow the workflow prompt format (see Content Conventions)
3. Include: Purpose, Trigger, Safety Level, Prompt, What it does
4. Ensure the exact count remains accurate (currently 28 numbered workflows)
5. Update to "29+ tested workflow prompts" in README.md only after the 29th workflow is added

### Task: Fix Broken Links

**When:** Internal links are broken or need updating

**Actions:**

1. Use **relative paths** from the current document's location
2. For Jekyll: Use `/docs/workshop/file.md` format for absolute paths
3. Test links by running Jekyll locally
4. Remember: Jekyll transforms `.md` to `.html` in output

### Task: Improve Facilitator Guide

**When:** Adding teaching tips, troubleshooting, or clarifications

**Actions:**

1. Keep the minute-by-minute timeline intact
2. Add troubleshooting under **"Common Issues"** section
3. Add teaching tips as **💡 Tip:** callouts
4. Add warnings as **⚠️ Warning:** callouts
5. Maintain the progressive complexity flow

### Task: Update Prerequisites

**When:** New requirements or setup steps are needed

**Actions:**

1. Update `README.md` (Prerequisites section)
2. Update `docs/workshop/gh-agentic-workflows-session.md` (Prerequisites section)
3. Update `docs/workshop/participant-handout.md` (Setup requirements)
4. Update `docs/workshop/quick-reference-card.md` if it affects quick reference
5. Ensure consistency across all documents

### Task: Add Translations

**When:** Adding localized versions of workshop materials

**Actions:**

1. Create new directory: `docs/workshop/[language-code]/`
2. Translate all core materials maintaining original structure
3. Update `docs/_config.yml` if needed for language support
4. Add language selection to `docs/index.md`
5. Update README.md to mention available languages

## Testing and Validation

### Before Committing Changes

1. **Markdown Validation:**
   - Check that all code blocks have closing backticks
   - Verify heading hierarchy (no skipped levels)
   - Ensure lists are properly formatted

2. **Link Testing:**
   - Start Jekyll server locally
   - Click through all internal links
   - Verify external links are valid

3. **Content Review:**
   - Timing still adds up correctly
   - Commands are accurate and tested
   - Examples work as described
   - No broken or outdated references

4. **Formatting Check:**
   - Consistent emoji usage
   - Proper code block language tags
   - Consistent heading styles
   - Proper spacing around headers

### Jekyll Build Validation

```bash
cd docs
bundle exec jekyll build
# Check for warnings or errors in output
```

If build succeeds without errors, the site will render correctly.

## Safety Guardrails for AI Agents

### Do Not Modify

- **LICENSE** - Legal document, should not be altered
- **Git history** - Never rewrite history on shared branches
- **Core workshop flow** - The progressive complexity structure is battle-tested

### Always Preserve

- **Workshop timing structure** - 2-hour format with specific breakpoints
- **Safety classifications** - Workflow risk levels (🟢🟡🔴)
- **Prerequisite accuracy** - Don't add dependencies that aren't truly needed
- **Cross-references** - When updating one document, check related documents

### Require Human Review

- Major structural changes to workshop materials
- Changes affecting workshop duration significantly
- New prerequisites or tool requirements
- Modifications to safety guidelines or best practices
- Removal of existing content

## Contributing Workflow

When making changes:

1. **Small changes** (typos, formatting, minor clarifications):
   - Make changes directly
   - Commit with clear message: "Fix: [description]"

2. **Medium changes** (new examples, updated instructions):
   - Review related documents for consistency
   - Test locally if affecting Jekyll site
   - Commit with clear message: "Update: [description]"

3. **Large changes** (new sections, restructuring, new features):
   - Check CONTRIBUTING.md for guidance
   - Consider impact on workshop timing
   - Test thoroughly
   - Document changes clearly
   - Commit with clear message: "Add: [description]" or "Refactor: [description]"

## File-Specific Guidance

### README.md

- Primary repository landing page
- Keep badges up to date
- Maintain clear navigation structure
- Include visual hierarchy with emojis
- Quick Start section should be truly quick (< 5 minutes to understand)

### CONTRIBUTING.md

- Guide for external contributors
- Includes PR guidelines and writing style
- Should welcome all skill levels
- Update when contribution process changes

### docs/workshop/facilitator-guide.md

- Most detailed document
- Minute-by-minute timeline is critical
- Include timing for every section
- Add troubleshooting proactively
- Include checkpoint questions for audience engagement

### docs/workshop/participant-handout.md

- Self-service reference for attendees
- Must work standalone (participants may not have facilitator)
- Include all commands, no assumptions
- Troubleshooting section should be comprehensive

### docs/workshop/example-workflow-prompts.md

- Growing library of patterns (currently 28 numbered workflows)
- Each prompt should be tested before adding
- Organize by category (Daily Operations, Continuous Improvement, etc.)
- Include safety levels for each
- Footer references CopilotAdventures as the practice repository (this is correct - it's the repo used during workshops)
- Footer references CopilotAdventures as the practice repository (this is correct - it's the repo used during workshops)

## Common Patterns to Recognize

### Progressive Complexity

The workshop follows this learning progression:

1. Simple status/reporting workflows
2. CI/CD helper workflows (coach, doctor)
3. Continuous improvement workflows (tests, docs)
4. Repository management workflows (triage, planning)
5. Advanced patterns (reuse, maintenance)

Maintain this progression when adding new content.

### Safety-First Approach

All workflow examples should include:

- Clear indication of what changes they make
- Appropriate safety level (🟢🟡🔴)
- Mention of human-in-the-loop when needed
- Explanation of potential risks

### Hands-On Focus

Workshop materials prioritize:

- Doing > Watching
- Practical examples > Theory
- Real repositories > Toy examples
- Immediate application > Future possibilities

## Version Control Practices

### Commit Message Format

Use conventional commits style:

- `Fix: [description]` - Bug fixes, typo corrections
- `Update: [description]` - Content improvements, clarifications
- `Add: [description]` - New content or features
- `Refactor: [description]` - Restructuring without changing meaning
- `Docs: [description]` - Documentation-only changes

### Branch Strategy

- `main` - Stable, workshop-ready materials
- Feature branches for significant changes
- Test locally before merging

## Integration Points

### External Resources Referenced

- **GitHub CLI** (`gh`) - Command-line tool for GitHub
- **GitHub Copilot** - AI pair programmer
- **GitHub Agentic Workflows** - The feature being taught
- **CopilotAdventures** - Example repository for practice

When updating materials, verify these resources are still current.

## Maintenance Checklist

### Quarterly Review

- [ ] Verify all external links still work
- [ ] Check if GitHub CLI commands have changed
- [ ] Confirm workshop timing is still accurate
- [ ] Review and update example workflow prompts
- [ ] Ensure prerequisites are current
- [ ] Check for new Jekyll theme updates

### After Each Workshop Delivery

- [ ] Collect facilitator feedback
- [ ] Update timing if sections ran long/short
- [ ] Add encountered issues to troubleshooting
- [ ] Improve unclear instructions
- [ ] Add new Q&A items if patterns emerge

## Meta: About This File

**Purpose:** Guide AI agents (like GitHub Copilot) in effectively managing this repository

**Update When:**

- Repository structure changes
- New documents are added
- Conventions change
- New maintenance patterns emerge

**Audience:** AI agents, automated tools, and contributors seeking to understand repository management patterns

---

**Last Updated:** March 4, 2026  
**Maintained By:** Repository contributors  
**Questions?** See CONTRIBUTING.md for how to suggest improvements to this guide
