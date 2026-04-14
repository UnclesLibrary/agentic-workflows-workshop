# GitHub Copilot Dev Days Workshop Materials

## "From Code to Automation: Mastering GitHub Agentic Workflows"

<div align="center">

![GitHub Copilot Dev Days](https://img.shields.io/badge/GitHub-Copilot%20Dev%20Days-blue)
![Workshop Duration](https://img.shields.io/badge/Duration-2.5%2B%20hours-green)
![Skill Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

**Complete workshop materials for teaching GitHub Agentic Workflows at community events**

[Overview](#-overview) •
[Quick Start](#-quick-start) •
[Materials](#-materials-included) •
[Usage](#-using-these-materials) •
[Contributing](#-contributing)

</div>

---

## 🎯 Overview

This repository contains comprehensive, battle-tested materials for delivering a 2.5+ hour hands-on workshop teaching **GitHub Agentic Workflows**—a revolutionary way to automate repository maintenance, continuous improvement, and development workflows using natural language and AI.

Perfect for **GitHub Copilot Dev Days** events, user groups, conferences, and team training sessions.

### What Participants Will Learn

- Write intelligent automation workflows in natural language (no YAML required)
- Implement continuous improvement patterns (tests, documentation, refactoring)
- Automate issue management and triage
- Build CI/CD coaching and diagnostics systems
- Create self-organizing, self-improving repositories
- Apply proper safety guardrails for AI automation

### Workshop Highlights

✨ **Progressive Learning** - Start simple, build sophistication naturally  
🎓 **Hands-on Practice** - Build real workflows on actual repositories  
🔒 **Safety First** - Teach proper guardrails and human-in-the-loop patterns  
🌍 **Community-Ready** - Designed for diverse audiences and skill levels  
📦 **Complete Package** - Everything needed from setup to follow-up

---

## 🚀 Quick Start

### For Event Organizers

1. **Review the materials**  
   Browse the [workshop materials](/docs/workshop/) for a complete overview

2. **Customize for your event**  
   Edit [gh-agentic-workflows-session.md](docs/workshop/gh-agentic-workflows-session.md) with your event details

3. **Prepare your venue**  
   Ensure WiFi, projector, and seating are ready for hands-on work

4. **Promote your workshop**  
   Use the event descriptions and session tags provided

### For Facilitators

1. **Study the facilitator guide**  
   [facilitator-guide.md](docs/workshop/facilitator-guide.md) has minute-by-minute instructions

2. **Practice the exercises**  
   Run through all exercises yourself first (allow 3+ hours for prep)

3. **Set up your demo environment**  
   Fork [CopilotAdventures](https://github.com/microsoft/CopilotAdventures) and test workflows

4. **Prepare backups**  
   Have screenshots, recordings, and backup examples ready

5. **Review the slide deck**  
   Build your presentation using [slide-deck-outline.md](docs/workshop/slide-deck-outline.md)

### For Participants

1. **Review prerequisites**  
   Check [participant-handout.md](docs/workshop/participant-handout.md) for required setup

2. **Bring your laptop**  
   With admin rights to install software

3. **Have your accounts ready**
   - GitHub account (free)
   - GitHub Copilot access (trial available)

4. **Print the quick reference**  
   [quick-reference-card.md](docs/workshop/quick-reference-card.md) for easy access during workshop

---

## 📦 Materials Included

| File                                                                             | Purpose                                         | Target Audience  |
| -------------------------------------------------------------------------------- | ----------------------------------------------- | ---------------- |
| [gh-agentic-workflows-session.md](docs/workshop/gh-agentic-workflows-session.md) | Event page description, learning outcomes       | Event Organizers |
| [facilitator-guide.md](docs/workshop/facilitator-guide.md)                       | Complete workshop delivery guide (9,000+ words) | Facilitators     |
| [participant-handout.md](docs/workshop/participant-handout.md)                   | Student reference with all commands             | Participants     |
| [example-workflow-prompts.md](docs/workshop/example-workflow-prompts.md)         | 28+ tested workflow patterns                    | Everyone         |
| [slide-deck-outline.md](docs/workshop/slide-deck-outline.md)                     | 15-slide presentation structure                 | Facilitators     |
| [quick-reference-card.md](docs/workshop/quick-reference-card.md)                 | One-page printable cheat sheet                  | Participants     |

### Content Overview

**Total Pages:** ~100+ pages of content  
**Preparation Time:** 3-4 hours for first-time facilitators  
**Delivery Time:** 2.5+ hours standard, extensible to 3+ hours  
**Exercise Count:** 11 progressive hands-on exercises  
**Workflow Patterns:** 28 ready-to-use examples

---

## 🎓 Using These Materials

### License & Usage

These materials are released under the MIT License. You are free to:

- ✅ Use for community events, workshops, and training
- ✅ Modify and customize for your audience
- ✅ Distribute to participants
- ✅ Create derivative works

**Attribution appreciated but not required.**

### Recommended Approach

1. **Don't change everything** - The materials are tested and work well as-is
2. **Customize minimally** - Add your personality and local examples
3. **Practice first** - Run through once before delivering
4. **Gather feedback** - Use participant feedback to improve
5. **Share back** - Contribute improvements via PR

### Customization Ideas

- **Add your branding** - Logo, colors, contact info
- **Localize content** - Language, cultural references, local examples
- **Adjust difficulty** - More or fewer advanced topics based on audience
- **Change timing** - Extend or compress based on available time
- **Add exercises** - Include organization-specific scenarios

---

## 🌟 Workshop Format

### Standard 2.5-Hour Format

```
0:00-0:15   Introduction & Concepts
0:15-0:30   Setup (CLI, repository, authentication)
0:30-2:00   Progressive Hands-on Exercises
              → Daily operations (standup reports)
              → CI/CD enhancement (coach & doctor)
              → Continuous improvement (tests, docs)
              → Issue management (triage, planning)
              → Advanced patterns (reuse, maintenance)
2:00-2:15   Wrap-up, Retrospective
2:15-2:30   Q&A and Open Discussion
```

### Dual Track Option (3-3.5 Hours)

- **Beginner Track** - Guided templates, understanding concepts
- **Advanced Track** - Build from scratch, sophisticated patterns
- **Shared Sessions** - Intro, setup, demo sharing, wrap-up

### Extended Format (Half Day)

Add:

- Break periods
- Team collaboration exercises
- Deeper dives into security and governance
- Participant presentations
- Office hours for individual projects

---

## 🏗️ Technology Stack

### What Participants Will Use

- **GitHub CLI** (`gh`) - Command line interface for GitHub
- **gh-aw Extension** - GitHub Agentic Workflows CLI
- **Git** - Version control
- **GitHub Account** - With Copilot access
- **VS Code** (optional) - For repository agent features

### What Workflows Run On

- **GitHub Actions** - Execution environment
- **GitHub Copilot API** - AI intelligence
- **GitHub API** - Repository interactions

### Prerequisites

- Windows, Mac, or Linux laptop
- Admin rights to install software
- Internet connection
- Modern web browser

---

## 📊 Success Metrics

### Workshop Outcomes

After completing this workshop, participants should be able to:

- [ ] Explain what GitHub Agentic Workflows are and why they matter
- [ ] Install and configure the gh-aw CLI
- [ ] Create workflows using all three methods (CLI, cloud, repo agent)
- [ ] Implement at least 5 different workflow patterns
- [ ] Apply appropriate safety guardrails
- [ ] Have a working repository with active automation
- [ ] Continue building workflows independently

### Facilitator Success Indicators

- **High engagement** - Most participants complete exercises
- **Positive energy** - Questions, excitement, discussion
- **Working demos** - Workflows actually produce results
- **Clear takeaways** - Participants know next steps
- **Community building** - Attendees connect with each other

---

## 🤝 Contributing

We welcome improvements and adaptations! Here's how to contribute:

### Reporting Issues

Found a problem? Please open an issue with:

- Which material has the issue
- What's wrong or unclear
- Suggested improvement
- Context (audience type, timing, etc.)

### Suggesting Improvements

Have an idea? Create an issue or PR with:

- Description of the improvement
- Why it would help
- Any testing you've done
- Impact on timing or flow

### Sharing Your Experience

Delivered the workshop? Please share:

- Number of participants
- What worked well
- What needed adjustment
- Questions that came up
- Feedback from attendees
- Photos/tweets (with permission)

### Contributing New Materials

Want to add content? Consider:

- **New workflow patterns** - Add to example-workflow-prompts.md
- **Advanced exercises** - Extend facilitator guide
- **Translations** - Localize materials
- **Slide decks** - Share your presentation
- **Videos** - Record and share (with permission)

---

## 🌍 Community

### GitHub Copilot Dev Days

This workshop is designed for the global **GitHub Copilot Dev Days** initiative:

- **Dates:** March 15 - May 15, 2026
- **Format:** Community-led, in-person events
- **Calendar:** [aka.ms/githubcopilotdevdays](https://aka.ms/githubcopilotdevdays)

### Connect & Share

- **Discussions:** Share experiences and ask questions
- **GitHub Next Discord:** [gh.io/next-discord](https://gh.io/next-discord)
- **Community Forum:** [GitHub Discussions](https://github.com/orgs/community/discussions/186451)
- **Social Media:** Tag `#GitHubCopilotDevDays`

### Related Resources

- **GitHub Agentic Workflows Docs:** [github.github.com/gh-aw](https://github.github.com/gh-aw/)
- **Peli's Agent Factory:** Blog with examples and patterns
- **CopilotAdventures:** Practice repository used in workshop
- **Workflow Library:** [github.com/githubnext/agentics](https://github.com/githubnext/agentics)

---

## 📅 Version History

- **v1.0** (March 2026) - Initial release for Copilot Dev Days 2026
  - Complete 2.5+ hour workshop
  - 7 comprehensive materials
  - 28 workflow patterns
  - Tested with pilot groups

---

## 📞 Support

### Questions About Materials

- **General questions:** Open an issue in this repository
- **Workshop delivery:** Join GitHub Next Discord
- **Content suggestions:** Submit a PR or issue

### Running Your Workshop

- **Event registration:** [GitHub Copilot Dev Days Form](https://aka.ms/githubcopilotdevdays/form)
- **Event calendar:** [Luma Calendar](https://aka.ms/githubcopilotdevdays)
- **Organizer resources:** [GitHub-Copilot-Dev-Days Repository](https://github.com/github/GitHub-Copilot-Dev-Days)

---

## 📄 License

MIT License - See LICENSE file for details.

**Summary:** Use freely, modify as needed, attribution appreciated.

---

## 🙏 Acknowledgments

These materials were created for the GitHub Copilot Dev Days 2026 community event series.

**Special Thanks:**

- GitHub Next team for GitHub Agentic Workflows
- GitHub Copilot team for the AI capabilities
- CopilotAdventures contributors for the practice repository
- Community organizers worldwide hosting events
- Early workshop participants for feedback

---

## 🚀 Ready to Get Started?

1. **Browse the [workshop materials](docs/workshop/)** - Understand what's included
2. **Review [facilitator-guide.md](docs/workshop/facilitator-guide.md)** - Learn the flow
3. **Practice the exercises** - Get hands-on experience
4. **Register your event** - Put it on the calendar
5. **Deliver with confidence** - You've got this!

---

<div align="center">

**Let's build the future of automated development together! 🚀**

Questions? Feedback? Want to share your workshop experience?  
[Open an issue](./issues) or [start a discussion](./discussions)

**Made with ❤️ for the GitHub Copilot community**

</div>
