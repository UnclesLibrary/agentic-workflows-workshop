# GitHub Agentic Workflows Workshop Materials

This directory contains comprehensive materials for delivering the "From Code to Automation: Mastering GitHub Agentic Workflows" workshop at GitHub Copilot Dev Days events.

## 📦 What's Included

### For Event Organizers

- **[gh-agentic-workflows-session.md](gh-agentic-workflows-session.md)** - Complete session description for event pages, including:
  - Event page copy
  - Learning outcomes
  - Target audience
  - Prerequisites
  - Materials needed
  - Follow-up resources

### For Facilitators

- **[facilitator-guide.md](facilitator-guide.md)** - Detailed 2-hour workshop guide with:
  - Minute-by-minute timeline
  - Setup instructions
  - Live coding demonstrations
  - Discussion prompts
  - Troubleshooting tips
  - Checkpoint questions
  - Common pitfalls to avoid

### For Participants

- **[participant-handout.md](participant-handout.md)** - Student reference guide containing:
  - All setup commands
  - Exercise instructions
  - Workflow creation patterns
  - Troubleshooting guide
  - Resource links
  - Quick command reference

### Resources

- **[example-workflow-prompts.md](example-workflow-prompts.md)** - Library of 28+ tested workflow prompts:
  - Daily operations (standups, health reports)
  - Continuous improvement (tests, refactoring)
  - CI/CD enhancement (coach, doctor)
  - Issue management (triage, planning)
  - Maintenance (dependencies, dead code)
  - Security & compliance
  - Community & communication
  - Advanced patterns

## 🎯 Workshop Overview

**Title:** From Code to Automation: Mastering GitHub Agentic Workflows  
**Duration:** 2 hours  
**Format:** Hands-on, progressive complexity  
**Prerequisites:** GitHub account, GitHub Copilot access, laptop

### Learning Progression

```
0:00-0:15   Introduction → Why agentic workflows matter
0:15-0:30   Setup → Install CLI, create repository, configure
0:30-1:45   Hands-on Exercises → Progressive complexity
              ├─ Simple workflows (daily status)
              ├─ Quality workflows (CI coach/doctor)
              ├─ Continuous improvement (tests, docs)
              ├─ Repository management (assistant, triage)
              ├─ Planning automation (/plan command)
              └─ Advanced patterns (reuse, maintenance)
1:45-2:00   Wrap-up → Retrospective, Q&A, next steps
```

### Key Teaching Concepts

1. **Three Creation Methods** (scaffold understanding)
   - CLI Wizard: Simple, template-based
   - Cloud Agent: Higher quality, documentation-aware
   - Repository Agent: Best quality, context-aware

2. **Progressive Complexity** (natural growth)
   - Start with obvious wins (daily standup)
   - Add value incrementally (CI help, tests)
   - Address emerging needs (issue management)
   - Build sophisticated systems (orchestration)

3. **Automation Requires Management** (meta-automation)
   - Show issues growing overwhelming
   - Solve with repository assistant
   - Demonstrate self-organizing systems

4. **Human-in-the-Loop** (guardrails)
   - AI proposes, humans decide
   - Review all auto-generated PRs
   - Approval gates for critical operations

## 🚀 Quick Start for Facilitators

### 1 Week Before Workshop

- [ ] Review all materials thoroughly
- [ ] Test all exercises in your own repository
- [ ] Customize examples to your audience
- [ ] Set up demo repository
- [ ] Test equipment (projector, WiFi)
- [ ] Print participant handouts (optional)

### 1 Day Before Workshop

- [ ] Run through entire workshop once
- [ ] Verify all workflows still work
- [ ] Check for updates to gh-aw CLI
- [ ] Prepare backup PAT tokens
- [ ] Charge laptop fully
- [ ] Download any needed resources

### Day of Workshop

- [ ] Arrive 30 minutes early
- [ ] Test all tech (projector, WiFi, demos)
- [ ] Have backup laptop ready
- [ ] Post WiFi info and links
- [ ] Welcome participants as they arrive

### During Workshop

- [ ] Use checkpoints to keep everyone together
- [ ] Encourage questions throughout
- [ ] Celebrate when workflows work
- [ ] Stay calm when demos fail (they will)
- [ ] Help struggling participants

### After Workshop

- [ ] Share resources with participants
- [ ] Collect feedback via survey
- [ ] Document lessons learned
- [ ] Update materials based on feedback
- [ ] Follow up with community

## 📋 Materials Checklist

### Digital Assets

- [ ] Facilitator guide (this repository)
- [ ] Participant handout (this repository)
- [ ] Example workflow prompts (this repository)
- [ ] Slide deck (create from slide-outline.md)
- [ ] Demo repository with working workflows
- [ ] Feedback survey link
- [ ] Resource links document

### Physical Setup

- [ ] Laptop (fully charged)
- [ ] Backup laptop
- [ ] Power strips/extension cords
- [ ] HDMI/display adapters
- [ ] Wireless presenter remote (optional)
- [ ] Printed handouts (optional)
- [ ] Whiteboard markers
- [ ] Sticky notes for questions

### Accounts & Access

- [ ] GitHub account (facilitator)
- [ ] GitHub Copilot license
- [ ] Demo repository prepared
- [ ] gh-aw CLI installed and tested
- [ ] PAT token created and tested
- [ ] Backup PAT tokens for emergencies

## 🎓 Using CopilotAdventures Repository

This workshop uses the [CopilotAdventures](https://github.com/microsoft/CopilotAdventures) repository as the foundation because:

1. **Multi-language**: C#, JavaScript, Python - shows workflows work across languages
2. **Simple codebase**: Easy to understand, focus on automation not domain logic
3. **Clear structure**: Well-organized, easy to find improvement opportunities
4. **Existing patterns**: Has solutions, tests, documentation to work with
5. **Educational**: Participants can continue using after workshop

### Why This Works

- **Immediate improvements**: Easy to spot missing tests, outdated docs
- **Clear examples**: Solution files are simple and understandable
- **Multiple tracks**: Beginners and advanced users find relevant exercises
- **Real value**: Participants leave with working automation
- **Continuation**: Can continue improving after workshop

## 💡 Customization Tips

### For Different Audiences

**Junior Developers:**

- Spend more time on setup
- Use more guided exercises
- Focus on simpler workflows
- Emphasize learning over sophistication

**Senior Developers:**

- Move faster through setup
- Focus on advanced patterns
- Encourage experimentation
- Discuss team adoption strategies

**DevOps/Platform Engineers:**

- Emphasize CI/CD patterns
- Cover security and compliance
- Discuss integration with existing tools
- Focus on organization-wide adoption

**Open Source Maintainers:**

- Focus on community management workflows
- Cover triage and communication patterns
- Discuss contributor engagement
- Address scaling challenges

### For Different Time Slots

**90 Minutes:**

- Skip advanced patterns section
- Combine exercises 4-6
- Shorter Q&A
- Provide resources for self-study

**3 Hours:**

- Add dual track (beginner/advanced)
- Include more experimentation time
- Add team discussion sessions
- Cover additional patterns

**Half Day (4 hours):**

- Add break periods
- Include team project work
- Cover advanced orchestration
- Have participants share creations

## 📚 Additional Resources

### For Facilitators

- [GitHub Agentic Workflows Docs](https://github.github.com/gh-aw/)
- [Peli's Agent Factory](https://github.github.com/gh-aw/blog/2026-01-12-welcome-to-pelis-agent-factory/)
- [GitHub Actions Documentation](https://docs.github.com/actions)
- [Copilot Dev Days Resources](https://github.com/github/GitHub-Copilot-Dev-Days)

### For Participants

- [Quick Start Guide](https://github.github.com/gh-aw/setup/quick-start/)
- [Security Architecture](https://github.github.com/gh-aw/introduction/architecture/)
- [Community Discussions](https://github.com/orgs/community/discussions/186451)
- [GitHub Next Discord](https://gh.io/next-discord)
- [Workflow Library](https://github.com/githubnext/agentics)

## 🤝 Contributing

Found something that works well? Have suggestions for improvements?

1. Test your changes in a real workshop setting
2. Document what worked and what didn't
3. Submit a PR with:
   - Clear description of change
   - Why it improves the workshop
   - Any facilitator notes
4. Share feedback in GitHub Discussions

## 📞 Support

**Questions about the workshop materials?**

- Open an issue in this repository
- Ask in GitHub Discussions
- Join GitHub Next Discord

**Running a workshop?**

- Follow GitHub Copilot Dev Days guidelines
- Register on the Luma calendar
- Share your experiences with the community

## 🎉 Success Stories

After successfully running this workshop, please share:

- Number of participants
- What worked well
- What needed adjustment
- Interesting workflows created
- Feedback from participants
- Photos/tweets (with permission)

We'd love to feature your event!

## 📄 License

These workshop materials are part of the CopilotAdventures repository and follow the same license terms.

---

**Created for:** GitHub Copilot Dev Days 2026  
**Workshop:** From Code to Automation: Mastering GitHub Agentic Workflows  
**Maintainers:** [Your name/team]  
**Last Updated:** March 4, 2026

**Happy automating! 🚀**
