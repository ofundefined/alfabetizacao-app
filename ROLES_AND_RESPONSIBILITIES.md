# Roles, Responsibilities, and Workflow

## Team Structure (MVP Phase)

### You (Lead Product & QA)
- **Responsibilities**:
  - Lead pedagogy decisions (alignment with Freire, Sr. Hélio's needs)
  - Qualify and review all work (code, content, design)
  - Make final decisions on direction and tradeoffs
  - Set up and manage Firebase + EAS build infrastructure
  - Facilitate user testing with Sr. Hélio and similar learners

- **Key decisions you own**:
  - Approve story content and reflection prompts
  - Vet code architecture and security
  - Prioritize features based on user feedback
  - Go/no-go decisions for releases

### Me (Pedagogy Content, Coding, UI/UX Design)
- **Responsibilities**:
  - Write and iterate on stories, phonetic lessons, reflection prompts
  - Design and implement React Native app (screens, navigation, offline mode)
  - Design UI/UX (wireframes, visual design, interaction patterns)
  - Implement backend (Node.js API, database schemas, TTS integration)
  - Write clear documentation for deployment and maintenance

- **Deliverables each week**:
  - Code (committed to GitHub with clear messages)
  - Design artifacts (Figma links or screenshots)
  - Content drafts (stories, phonics sequences)
  - Documentation (setup guides, architecture decisions)

### You (Firebase & EAS Setup)
- **Responsibilities**:
  - Create Firebase project and Firestore schema
  - Set up authentication (email/phone code)
  - Configure EAS Build for iOS/Android app distribution
  - Manage app store submissions (Apple TestFlight, Google Play)
  - Set up CI/CD pipeline (GitHub Actions)

---

## Weekly Workflow

### Monday: Planning
1. **I** draft weekly plan: what's the user story/feature?
2. **You** review and approve priorities
3. **Both** discuss pedagogy/UX decisions
4. **Output**: Agreed scope for the week

### Tuesday–Thursday: Execution
1. **I** build: code + content + design
2. **I** commit to GitHub with clear messages
3. **You** receive summary of progress (async)
4. **Output**: Working features (or drafts for feedback)

### Friday: Review & Iteration
1. **I** demo work (video, screenshots, or live session)
2. **You** provide feedback and approve/iterate
3. **Both** identify blockers or open questions
4. **Output**: Clear direction for next week

### Every 2 Weeks: User Testing
1. **You** arrange session with Sr. Hélio (or similar learner)
2. **I** prepare prototype/current build
3. **You** lead session; I observe and take notes
4. **Both** synthesize insights and adjust priorities
5. **Output**: Updated roadmap based on learner feedback

---

## Decision Rights

| Area | Owner | Can Override |
|------|-------|--------------|
| Pedagogy direction | You | — |
| Content (stories, prompts) | I draft, you approve | You (final say) |
| UI/UX design | I design, you review | You (final say) |
| Code architecture | I design, you review | You (for security/complexity) |
| Infrastructure (Firebase, EAS) | You (setup & config) | — |
| Feature prioritization | I recommend, you decide | You (final say) |
| User research & testing | You facilitate | — |
| Launch timing | I recommend, you decide | You (final say) |

---

## Communication

- **GitHub Issues**: Feature requests, bugs, tasks
- **GitHub Discussions**: Design decisions, pedagogy debate, architecture questions
- **Weekly async updates**: Sunday evening → Friday morning (text + links)
- **Video review**: Every 2 weeks (30–60 min)
- **Slack/Discord**: For urgent blockers only

---

## Backlog Management

### Local + Notion Sync
- **Local**: `/Users/hada/Projects/OF/alfabetizacao-app/LOCAL_BACKLOG.md` (tracks sprints)
- **Notion**: https://www.notion.so/App-de-alfabetiza-o-freiriano-3460c05ece5180be9191f906cb97339b (shared reference)
- **GitHub Issues**: Developer tasks (linked to Notion cards)

### Weekly Backlog Update
1. **Friday**: I review completed items, update status
2. **Sunday**: You review and approve status changes
3. **Notion**: You update public-facing backlog
4. **GitHub**: Issues closed/updated automatically

---

## Content Creation Workflow

### Story Writing (Example: "O Dia de Hélio")

**I draft**:
```
A madrugada. Hélio acorda.
Avó ainda dorme.
Ele abre a porta...
[~50 words using phonetics A–E]
```

**You review**:
- ✓ Reflects Sr. Hélio's real life?
- ✓ Phonetics match lesson plan?
- ✓ Reflection prompt encourages conscientization?
- ✓ Respectful and dignified tone?

**Feedback loop**:
- You: "Change 'cansado' to 'lutando' — more agency"
- I iterate and resubmit
- Repeat until approved

**Integration**:
- I add to app data (`src/data/stories.json`)
- Firebase sync in backend
- Ready for UI rendering

---

## Testing & QA

### Unit Testing (My responsibility)
- Tests for TTS, offline sync, phonetic matching
- Tests for Firebase queries, auth flow
- Minimum 80% code coverage

### User Testing (Your facilitation)
- Schedule bi-weekly with Sr. Hélio or similar
- You lead session, observe his behavior
- I take notes on UX issues, content clarity
- We iterate immediately (sometimes same day)

### QA Before Release
- I test on Android 11–14, iOS 14–16
- You do final approval
- We tag release in GitHub
- EAS Build packages for distribution

---

## Escalation Path

If I'm blocked or uncertain:
1. **I** post question/decision point in GitHub Discussions
2. **You** respond within 24 hours
3. **If complex**: Schedule 15-min sync
4. **Resolution**: Decision documented in GitHub, I proceed

---

## Definition of Done

For each feature/story:

**Code**:
- [ ] Committed to main branch
- [ ] Tests pass (unit + integration)
- [ ] No console warnings
- [ ] Offline-first (data cached locally)
- [ ] Accessibility review (color contrast, text size, touch targets)
- [ ] Documented in README or ARCHITECTURE.md

**Content**:
- [ ] Written, reviewed, approved by you
- [ ] Integrated into app
- [ ] TTS tested (sounds natural)
- [ ] Reflection prompt tested (elicits thoughtful response)

**Design**:
- [ ] Figma mockup approved by you
- [ ] Implemented in React Native
- [ ] Tested on real device
- [ ] Follows design system (colors, typography, spacing)

**User Testing**:
- [ ] Shared with Sr. Hélio or similar
- [ ] Feedback documented
- [ ] Issues logged and prioritized

---

## Success Metrics (MVP)

We succeed when:
- Sr. Hélio completes 3+ letters and returns (7-day retention)
- He reads a real document (contract, letter) with app support
- His reflection prompts show growing critical consciousness
- Build time < 30 minutes (local dev loop)
- App runs offline without crashes
- 5+ beta testers report willingness to continue learning

---

## How You Qualify My Work

**Code review checklist**:
- ✓ Does it solve the stated problem?
- ✓ Is it maintainable (clear naming, comments)?
- ✓ Does it follow React Native conventions?
- ✓ Is it secure (no hardcoded secrets, input validation)?
- ✓ Does it work offline?

**Content review checklist**:
- ✓ Reflects Sr. Hélio's real life?
- ✓ Aligned with Freiriano pedagogy?
- ✓ Respectful and dignifying tone?
- ✓ Phonetics match lesson plan?
- ✓ Reflection prompt is open-ended and thoughtful?

**Design review checklist**:
- ✓ Large text (18pt+), high contrast?
- ✓ Simple navigation (minimal taps)?
- ✓ Touch targets adequate for older hands (48pt+)?
- ✓ Consistent with design system?
- ✓ Tested with accessibility tools?

If I submit something that doesn't meet these criteria, you reject it and I iterate. **Your approval is the gate to production.**

---

## Handoff (End of MVP Phase)

When MVP is complete and ready for wider launch:
- I provide:
  - Full source code (well-documented)
  - Architecture decisions (ARCHITECTURE.md)
  - Deployment guide (INFRASTRUCTURE.md)
  - Content pipeline documentation
  - Test suite with 80%+ coverage
  - Figma design system file
- You take:
  - Product leadership and strategy decisions
  - Ongoing stakeholder management
  - Feature prioritization based on market feedback
- Transition to team or next phase of development

---

## Questions Before We Start?

- Any role clarifications needed?
- Any communication preferences (Slack vs Discord vs GitHub)?
- How often do you want updates (daily, weekly, bi-weekly)?
- Who else should be looped in (other stakeholders, advisors)?
