# Local Backlog & Sprint Tracking

## Notion Source of Truth
**Shared backlog**: https://www.notion.so/App-de-alfabetiza-o-freiriano-3460c05ece5180be9191f906cb97339b?source=copy_link

This document tracks **local sprint progress** and **detailed technical tasks**. Notion is the shared reference.

---

## Current Phase: MVP (Weeks 1–8)

### Sprint 1: Foundation & Setup (Weeks 1–2)

**Status**: Not Started

**Objective**: Design system, content foundation, tech setup

#### Tasks

- [ ] **Design**: Create UI kit in Figma
  - [ ] Color palette (dark, accessible)
  - [ ] Typography (Space Grotesk, Inter, JetBrains Mono)
  - [ ] Component library (Button, Card, Input, etc.)
  - [ ] Wireframes for onboarding + 3 key screens
  - **Owner**: Me (Design) | **Review**: You | **Deadline**: End of Week 1

- [ ] **Content**: Draft stories and phonics sequences
  - [ ] Story 1: "O Dia de Hélio" (50 words, letters A–E)
  - [ ] Story 2: "Carta para Mãe" (60 words, letters F–J)
  - [ ] Phoneme sequence (letters A–J with 5 words each)
  - [ ] Reflection prompts (5–10 open-ended questions)
  - **Owner**: Me (Content) | **Review**: You | **Deadline**: End of Week 1

- [ ] **Tech**: Initialize project
  - [ ] React Native (Expo) scaffold
  - [ ] TypeScript setup
  - [ ] Firebase project created
  - [ ] Firestore schema designed
  - [ ] Local SQLite for offline mode configured
  - **Owner**: Me (Dev) | **Review**: You | **Deadline**: End of Week 1

- [ ] **Infrastructure**: Docker & deployment planning
  - [ ] docker-compose.yml drafted (INFRASTRUCTURE.md created ✓)
  - [ ] Nginx reverse proxy config ready
  - [ ] Database initialization script ready
  - **Owner**: You (Infrastructure) | **Deadline**: End of Week 1

#### Blockers / Questions
- None yet

---

### Sprint 2: Core Screens (Weeks 3–4)

**Status**: Not Started (depends on Sprint 1)

**Objective**: Onboarding, Letter A, Story reader, Progress dashboard working end-to-end

#### Tasks

- [ ] **Frontend: Onboarding**
  - [ ] Screen 1: Welcome (name input)
  - [ ] Screen 2: Motivation (radio buttons)
  - [ ] Screen 3: Ready (summary)
  - [ ] State persistence (localStorage)
  - **Owner**: Me (Dev) | **Deadline**: Week 3, Mon

- [ ] **Frontend: Letter A Lesson**
  - [ ] Letter display + pronunciation button (TTS)
  - [ ] 5 word cards (image, text, pronunciation)
  - [ ] Next button + navigation logic
  - **Owner**: Me (Dev) | **Deadline**: Week 3, Wed

- [ ] **Frontend: Story Reader**
  - [ ] Render formatted story text
  - [ ] Word tap → pronunciation
  - [ ] Read aloud button (full story TTS)
  - [ ] Reflection prompt (open text input)
  - **Owner**: Me (Dev) | **Deadline**: Week 3, Fri

- [ ] **Frontend: Progress Dashboard**
  - [ ] Visual progress bar (X/10 letters)
  - [ ] Unlocked badges
  - [ ] Stories completed count
  - **Owner**: Me (Dev) | **Deadline**: Week 4, Mon

- [ ] **Backend: Firestore integration**
  - [ ] User profile schema
  - [ ] Lesson data seeding
  - [ ] Story data seeding
  - [ ] Reflection submission endpoint
  - [ ] Progress calculation logic
  - **Owner**: Me (Dev) | **Deadline**: Week 3, Fri

- [ ] **Backend: TTS & Audio**
  - [ ] Expo Speech integration (Portuguese)
  - [ ] Audio caching (local file system)
  - [ ] Fallback if TTS unavailable
  - **Owner**: Me (Dev) | **Deadline**: Week 3, Thu

- [ ] **QA: Sprint 2 Review**
  - [ ] Test onboarding flow on device
  - [ ] Test Letter A on Android + iOS
  - [ ] Test story reader + reflection input
  - [ ] Check offline mode (disable internet, verify load)
  - **Owner**: You (QA) | **Deadline**: Week 4, Fri

#### Blockers / Questions
- None yet

---

### Sprint 3: Expansion & Polish (Weeks 5–6)

**Status**: Not Started (depends on Sprint 2)

**Objective**: Add letters B–J, spaced repetition, user testing

#### Tasks

- [ ] **Content: Letters B–J**
  - [ ] Write 5 words per letter
  - [ ] Create/source images
  - [ ] Record/generate audio
  - **Owner**: Me (Content) | **Deadline**: Week 5, Fri

- [ ] **Frontend: Lessons B–J**
  - [ ] Reusable lesson component
  - [ ] Add letters to navigation
  - [ ] Test progression
  - **Owner**: Me (Dev) | **Deadline**: Week 5, Wed

- [ ] **Backend: Spaced Repetition**
  - [ ] Review scheduling (3 days, 7 days, 14 days)
  - [ ] Notification prompts (if app allows push)
  - [ ] Store review history
  - **Owner**: Me (Dev) | **Deadline**: Week 6, Mon

- [ ] **User Testing: Sr. Hélio Session**
  - [ ] Schedule session (Week 5 or 6)
  - [ ] Prepare prototype build
  - [ ] Observe + take notes on UX
  - [ ] Collect feedback on content
  - **Owner**: You (Testing) + Me (Observation) | **Deadline**: Week 6, Wed

- [ ] **Iterate based on feedback**
  - [ ] Fix top 3 UX issues
  - [ ] Refine content based on Sr. Hélio's responses
  - **Owner**: Me (Dev) | **Deadline**: Week 6, Fri

#### Blockers / Questions
- TBD based on Sprint 2 results

---

### Sprint 4: Launch Prep (Weeks 7–8)

**Status**: Not Started (depends on Sprint 3)

**Objective**: Final QA, app store setup, beta launch

#### Tasks

- [ ] **Final Testing**
  - [ ] Android 11, 12, 13, 14 compatibility
  - [ ] iOS 14, 15, 16 compatibility
  - [ ] Low-end device performance test
  - [ ] Slow network test (throttle to 2G)
  - [ ] Crash reporting (Sentry) configured
  - **Owner**: You (QA) | **Deadline**: Week 7, Wed

- [ ] **Infrastructure: Deploy to VPS**
  - [ ] Docker containers built and tested
  - [ ] Nginx proxy routing verified
  - [ ] SSL certificates installed
  - [ ] Database backed up
  - **Owner**: You (Infrastructure) | **Deadline**: Week 7, Thu

- [ ] **App Store Submissions**
  - [ ] Apple TestFlight setup
  - [ ] Google Play Console setup
  - [ ] App store copy (description, screenshots, icon)
  - [ ] Privacy policy + terms of service
  - **Owner**: You (App Store) | **Deadline**: Week 7, Fri

- [ ] **Beta Launch**
  - [ ] Invite 10–20 testers
  - [ ] Collect feedback (crashes, usability, content)
  - [ ] Fix critical bugs (P0)
  - **Owner**: You (Product) | **Deadline**: Week 8, Fri

- [ ] **Public Launch Prep**
  - [ ] Press kit (announcement, story of Sr. Hélio)
  - [ ] Social media ready
  - [ ] Notion backlog migrated to remote backlog (next phase)
  - **Owner**: You (Product) + Me (Documentation) | **Deadline**: End of Week 8

#### Blockers / Questions
- TBD based on user testing

---

## Completed Sprints

(None yet — this is the start)

---

## Open Questions

1. **User Testing**: How do we reach Sr. Hélio for testing? Do you have contacts?
2. **Content Voice**: Portuguese from which region? (Bahian expressions vs. São Paulo?) Any preferences?
3. **Notification**: Do we want push notifications for review reminders, or just in-app prompts?
4. **Mentor Portal**: Should MVP include a mentor dashboard to read reflections, or is that Phase 2?
5. **Monetization**: Completely free, or freemium later?

---

## Key Dates

| Milestone | Date | Owner |
|-----------|------|-------|
| Design kit + wireframes | Week 1 end | Me |
| Tech setup complete | Week 1 end | Me + You (Firebase) |
| Onboarding flow working | Week 3 start | Me |
| First user test | Week 5–6 | You |
| TestFlight/Play Store | Week 7 start | You |
| Beta launch | Week 8 | You |

---

## How to Update This

- **Weekly**: I update task progress (status, % complete, blockers)
- **Friday review**: You review and approve updates
- **Notion sync**: You propagate to Notion for stakeholders
- **GitHub**: Link tasks to GitHub Issues (automated)

---

## Template for Weekly Update (Fridays)

```
## Week X Recap (Mon–Fri)

### Completed ✅
- [ ] Task 1 (Owner: Me)
- [ ] Task 2 (Owner: You)

### In Progress 🔄
- Task 3 (70% done, no blockers)

### Blocked 🚨
- Task 4 (waiting for Firebase credentials)

### For Your Review
- [Figma link] Onboarding wireframes
- [GitHub PR] TTS integration

### Next Week Plan
- Task 5, 6, 7

### Metrics
- Code lines: +2,500 (mostly test coverage)
- Commits: 12
- Issues opened: 2 (TTS Portuguese quality)
```

---

## Sprint Retrospective Template (End of Every 2 Weeks)

```
## Retro: Sprint X

### What Went Well
- Design system adoption was smooth

### What Could Improve
- Initial Firebase setup took longer than expected

### Blockers / Learnings
- Portuguese TTS from Expo has slight accent issues

### Adjustments for Next Sprint
- Book TTS QA earlier
- Allocate extra time for Firebase schema design
```
