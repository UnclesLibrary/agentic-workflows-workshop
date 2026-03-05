# Slide Deck Outline

## GitHub Agentic Workflows Workshop Introduction

**Duration:** 15 minutes  
**Format:** Presentation with demos  
**Tool:** PowerPoint, Google Slides, or Keynote

---

## Slide 1: Title Slide

**Title:** From Code to Automation: Mastering GitHub Agentic Workflows

**Subtitle:** GitHub Copilot Dev Days 2026

**Visual:** GitHub Copilot logo + Agentic Workflows branding

**Bottom:** Your name, Date, Location

**Speaker Notes:**

- Welcome everyone
- Introduce yourself
- Set tone: hands-on, practical, fun

---

## Slide 2: What We'll Build Today

**Title:** Your Repository, Supercharged

**Visual:** Before/After comparison

**Before:**

- Manual standup reports
- Forgotten documentation
- Overwhelming issues
- CI failures surprise you
- Repetitive testing work

**After:**

- Automated daily insights ✅
- Self-updating docs ✅
- Organized, triaged issues ✅
- Proactive CI coaching ✅
- Continuous test improvements ✅

**Speaker Notes:**

- This is what you'll build in 2 hours
- On YOUR repository that you can keep using
- Real automation with immediate value

---

## Slide 3: The Problem

**Title:** The Developer's Dilemma

**Visual:** Developer overwhelmed with tasks

**Key Points:**

- We know what makes code better (tests, docs, refactoring)
- But we're always "too busy" to do it
- DevOps/CI/CD is powerful but complex
- GitHub Actions requires YAML expertise
- Manual repository maintenance is tedious
- Documentation drifts out of sync
- Issues pile up faster than we can triage

**Quote:** "I'll add tests after this feature..." (We never do)

**Speaker Notes:**

- Show of hands: Who has technical debt from "I'll do it later"?
- We all know we should do better, but time is limited
- The problem isn't knowledge, it's execution

---

## Slide 4: The Dream

**Title:** What If Automation Could...

**Visual:** Magic wand over code

**Bullet Points:**

- Write tests for you daily
- Keep documentation synchronized
- Triage issues intelligently
- Coach your CI/CD to prevent failures
- Plan features by breaking them into tasks
- Support your standups with insights
- All while you sleep

**And you just describe what you want in plain English?**

**Speaker Notes:**

- This sounds like science fiction
- But it's real and available today
- That's what we're here to learn

---

## Slide 5: The Solution

**Title:** GitHub Agentic Workflows

**Visual:** GitHub Agentic Workflows logo/diagram

**Three Key Points:**

1. **Write workflows in Natural Language (Markdown)**
   - No complex YAML required
   - Just describe what you want

2. **AI Agents Execute on GitHub Actions**
   - Understand your repository
   - Make intelligent decisions
   - Create PRs, issues, comments

3. **Human-in-the-Loop**
   - AI proposes, you approve
   - Guardrails and safety built-in
   - Full transparency

**Speaker Notes:**

- This bridges AI capabilities with practical automation
- Not replacing developers, amplifying them
- You provide direction, AI handles execution

---

## Slide 6: Live Demo - Simple Workflow

**Title:** See It In Action

**Demo:** Show actual workflow file

**Markdown Example:**

```markdown
# Daily Standup Report

Run every morning at 9 AM and create an issue summarizing:

- Commits from yesterday
- Pull requests needing review
- Issues created or closed
- Failed CI/CD runs

Title: "Daily Standup - [date]"
```

**Then Show:** The resulting issue created by the workflow

**Speaker Notes:**

- That's the entire workflow
- No YAML, no complex configuration
- AI figures out how to query APIs, format data, create issue
- You describe WHAT you want, AI figures out HOW

---

## Slide 7: How It Works

**Title:** Behind the Scenes

**Visual:** Architecture diagram

**Flow:**

1. You write workflow in markdown
2. GitHub Actions triggers on schedule/event
3. AI agent reads your description
4. Agent analyzes repository context
5. Agent executes using safe-outputs
6. Results appear (issues, PRs, comments)
7. You review and approve

**Guardrails:**

- Read-only by default
- Writes through sanitized safe-outputs
- Sandboxed execution
- Human approval gates optional

**Speaker Notes:**

- Runs in GitHub Actions (familiar environment)
- Multiple layers of safety
- You're always in control

---

## Slide 8: Three Ways to Create Workflows

**Title:** Quality Ladder

**Visual:** Staircase diagram

**Level 1: CLI Wizard** (Good)

- `gh aw create`
- Guided prompts
- Template substitution
- Great for learning

**Level 2: Cloud Agent** (Better)

- Reference documentation
- Higher quality results
- Works before repository initialized
- Production-ready

**Level 3: Repository Agent** (Best)

- After `gh aw init`
- Context-aware
- Understands your codebase
- Highest quality results

**Speaker Notes:**

- Today you'll experience all three
- Start simple, progress to sophisticated
- Each has its place

---

## Slide 9: Real-World Use Cases

**Title:** What Can You Build?

**Visual:** Grid of icons/screenshots

**Daily Operations:**

- Standup summaries
- Health reports
- Sprint retrospective data

**Continuous Improvement:**

- Add 3 tests per day
- Refactor complex code
- Update documentation

**CI/CD Enhancement:**

- Proactive coaching before failures
- Diagnostic analysis after failures
- Performance regression detection

**Issue Management:**

- Intelligent triage
- Planning with `/plan` command
- Repository assistant

**Advanced:**

- Multi-repo orchestration
- Workflow maintenance
- Security compliance

**Speaker Notes:**

- These are all real workflows we'll build or see today
- Start simple, add complexity as needed
- The possibilities are endless

---

## Slide 10: The Learning Journey Today

**Title:** Workshop Roadmap

**Visual:** Progressive path diagram

**Timeline:**

```
0:00  ← You are here (Introduction)
0:15  Setup (tools & repository)
0:30  First workflow (success!)
0:45  CI Coach & Doctor
1:05  Repository initialization
1:15  Issue management
1:30  Advanced patterns
2:00  Wrap-up & next steps
```

**Learning Pattern:**

1. Start simple (daily status)
2. Add value (CI help, tests)
3. Manage complexity (assistant)
4. Go advanced (orchestration)

**Speaker Notes:**

- Progressive complexity matches natural adoption
- Each step builds on previous
- No one jumps in the deep end
- You'll see patterns you can apply immediately

---

## Slide 11: Why CopilotAdventures?

**Title:** Your Practice Repository

**Visual:** CopilotAdventures logo/screenshot

**Why Perfect for Workshop:**

- ✅ Multi-language (C#, JavaScript, Python)
- ✅ Simple codebase (easy to understand)
- ✅ Clear improvement opportunities
- ✅ Well-structured
- ✅ Existing patterns to enhance
- ✅ Educational content
- ✅ You can continue using after

**What You'll Do:**

- Create your own repository from CopilotAdventures
- Add automation workflows
- See immediate improvements
- Keep improving after workshop

**Speaker Notes:**

- Not toy examples - real repository
- But simple enough to focus on automation
- Easy to spot what needs improvement
- You'll own it and can continue after

---

## Slide 12: Safety & Guardrails

**Title:** Built for Trust

**Visual:** Shield icon with checkmarks

**Security Layers:**

1. **Read-only by default**
   - Workflows can only read repository
2. **Safe-outputs for writes**
   - All writes sanitized and validated
3. **Sandboxed execution**
   - Isolated environment
4. **Network isolation**
   - Control external access
5. **Human approval gates**
   - You decide what gets merged
6. **SHA-pinned dependencies**
   - Supply chain security

**Golden Rule:** AI proposes, humans decide

**Speaker Notes:**

- Safety is foundational, not bolted on
- Multiple layers of protection
- You're always in control
- Review all auto-generated PRs before merging

---

## Slide 13: What Success Looks Like

**Title:** Your Future Repository

**Visual:** Dashboard showing healthy metrics

**Metrics Improving:**

- 📈 Test coverage climbing weekly
- 📚 Documentation always current
- 🎯 Issues triaged within minutes
- ✅ CI/CD success rate improving
- 🚀 Features broken into clear tasks
- 👥 Team velocity increasing
- 😊 Developer happiness up

**The Secret:**

- AI handles repetitive work
- You focus on creative work
- Continuous improvement on autopilot
- Self-organizing repository

**Speaker Notes:**

- This is achievable in weeks, not months
- Start small, let it grow
- Compound improvements over time
- Natural evolution, not forced transformation

---

## Slide 14: Questions Before We Start?

**Title:** Ready to Build?

**Visual:** Excited developer at keyboard

**Quick Questions:**

- Any concerns about the technology?
- Questions about use cases?
- Worried about safety?
- Need any clarification?

**What's Next:**

- Setup (15 minutes)
- Then hands-on coding!
- Stop me anytime with questions

**Speaker Notes:**

- Address any concerns now
- Set expectations: some things will break (that's OK!)
- Emphasize: hands-on, learn by doing
- We're all figuring this out together

---

## Slide 15: Let's Get Started!

**Title:** Setup Time

**Visual:** Checklist

**Next 15 Minutes:**

1. Install GitHub CLI
2. Install gh-aw extension
3. Authenticate with GitHub
4. Create your repository
5. Configure permissions
6. Get your PAT token

**Resources:**

- Participant handout has all commands
- Projected on screen
- Help each other
- Raise hand if stuck

**Let's go! 🚀**

**Speaker Notes:**

- Switch to terminal/live demo
- Walk through setup step-by-step
- Keep energy up
- Celebrate when people succeed

---

## Additional Slide Ideas (Optional)

### Slide: Team Adoption Strategy

- Start with one workflow
- Demonstrate value
- Get buy-in organically
- Scale gradually
- Measure impact

### Slide: Cost Considerations

- Runs on GitHub Actions minutes
- Typically <5 minutes per run
- Set spending limits
- Compare to manual effort cost
- ROI is usually immediate

### Slide: Integration with Existing Tools

- Works with GitHub Actions
- Can trigger external systems
- Webhook integration
- API extensibility
- MCP server connections

### Slide: Common Questions

- "Will this replace developers?" No—amplifies them
- "What if AI makes mistakes?" Human review always
- "Can I customize workflows?" Absolutely
- "Does it work with private repos?" Yes
- "How do I get team buy-in?" Start small, show value

---

## Presentation Tips

### Before Each Slide

- Pause and let audience absorb
- Make eye contact
- Check for confused faces
- Invite questions

### During Demos

- Test beforehand
- Have backup screenshots if live fails
- Explain what you're doing
- Show, don't just tell

### Energy Management

- Start with enthusiasm
- Vary your tone and pace
- Use humor when appropriate
- Show your genuine excitement

### Timing

- 1-1.5 minutes per slide
- Don't rush the demo slide
- Leave buffer for questions
- Be ready to skip slides if running behind

---

## Visual Design Suggestions

### Color Scheme

- GitHub colors (black, white, #0366d6)
- Accent with green for success
- Red sparingly for problems
- High contrast for readability

### Typography

- Large, readable fonts (min 24pt)
- Sans-serif for body (Segoe UI, Helvetica)
- Monospace for code (Consolas, Monaco)
- Bold for emphasis

### Images

- High resolution
- Relevant to content
- Not stock photos (use real screenshots)
- Consistent style throughout

### Layout

- Clean and uncluttered
- One idea per slide
- Plenty of white space
- Consistent formatting

---

## Backup Slides (Have Ready)

### If Technical Demo Fails

- Screenshot of successful workflow run
- Pre-recorded video demo
- Diagram showing the process

### For Advanced Questions

- Architecture deep dive
- Security model details
- Pricing breakdown
- Roadmap and future features

### Success Stories

- Real-world examples
- Team testimonials
- Metrics from actual usage
- Community creations

---

## Notes for Delivery

### Practice

- Rehearse full presentation 2-3 times
- Time yourself
- Practice transitions
- Prepare for common questions

### Backup Plans

- Have demo recorded as backup
- Prepare for tech failures
- Have extra time in schedule
- Stay calm if things break

### Audience Engagement

- Ask questions throughout
- Encourage interaction
- Use show of hands
- Make eye contact
- Read the room

### Flexibility

- Skip slides if running behind
- Expand on areas of interest
- Adapt to audience level
- Take tangents if valuable

---

**Slide Deck Version:** 1.0  
**Last Updated:** March 4, 2026  
**For:** GitHub Copilot Dev Days Workshop  
**Duration:** 15 minutes

**Remember:** Your enthusiasm is contagious. Show your genuine excitement about this technology and the audience will feel it too!
