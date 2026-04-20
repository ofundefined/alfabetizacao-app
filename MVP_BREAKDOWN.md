# MVP Breakdown — Caminho das Letras

Some audio chat and mnemonics images with text must be the leaver since the user does not know how to read. 

## Phase 1: Foundation (Weeks 1–2)

### Design & UX
- [ ] Wireframe key screens (Figma)
  - Onboarding (3 screens)
  - Lesson screen (letter + words)
  - Story screen
  - Progress dashboard
- [ ] Design system: typography, colors, touch targets (large!)
- [ ] Accessibility audit: color contrast, font sizes, spacing

### Technical Setup
- [ ] Initialize React Native project (Expo)
- [ ] Set up Firebase: Auth, Firestore, Storage
- [ ] Create folder structure:
  ```
  src/
    screens/      # Onboarding, Lesson, Story, Progress
    components/   # Reusable UI (Button, Card, etc)
    services/     # Firebase, TTS, offline sync
    data/         # Lessons, stories, phoneme sequences
    utils/        # Helpers
    types/        # TypeScript definitions
  ```
- [ ] Set up EAS Build for iOS/Android packaging

### Content Creation
- [ ] Define 10-letter phoneme sequence (A–J) with IPA
- [ ] Write 5 words per letter (with images/illustrations)
- [ ] Write 2 sample stories: "O Dia de Hélio" + "Carta para Mãe"
- [ ] Create audio recordings (TTS in Portuguese)
- [ ] Prepare reflection prompts

---

## Phase 2: Core Features (Weeks 3–4)

### Screens

**1. Onboarding (4 steps)**
```
Step 1: Welcome
  Subtitle: "Comece sua jornada de letras aqui"
  Button: "Começar"

Step 2: Name
  Input: "Qual é seu nome?"
  Button: "Próximo"

Step 3: Motivation
  Radio buttons:
    - Ler contrato de trabalho
    - Ler cartas da família
    - Ler receita
    - Outra razão
  Button: "Próximo"

Step 4: Ready
  Summary: "Bem-vindo, [Name]!"
  Button: "Começar a aprender"
```

**2. Lesson Screen (Letter A)**
```
Header: "Letra A" (large, 24pt)
Subtitle: "Sons do A"

Audio button: 🔊 "Ouça a letra"

Word cards (5):
┌─────────────────────┐
│ ATÓ                │
│ [image of hammer]  │
│ 🔊 Tap to hear    │
└─────────────────────┘
(repeat for ABRE, AVÓ, ATO, ABACAXI)

Bottom: "Próximo" button

Reflection prompt (collapsible):
"Como você se sente aprendendo?"
[Open-ended text input]
```

**3. Story Screen ("O Dia de Hélio")**
```
Title: "O Dia de Hélio"
Text (formatted, large):
  "A madrugada. Hélio acorda.
   Avó ainda dorme.
   Ele abre a porta."
   [etc, ~50 words]

Read aloud: 🔊 button
Tap word: tap any word → hear pronunciation

Bottom reflection:
"Você também trabalha?
 Fale sobre seu dia."
[Text input]
```

**4. Progress Screen**
```
Title: "Seu Progresso"

Visual progress bar:
████░░░░░░ 4 de 10 letras

Learned letters (unlocked badges):
🔵 A  🔵 B  🔵 C  🔵 D  ⭕ E (grayed)

Stories completed:
✅ O Dia de Hélio

Reflection count: 4 respostas

Next: "Aprenda a letra E"
```

---

### Implementation Checklist

#### Frontend (React Native)
- [ ] Navigation stack: Onboarding → App → Lesson
- [ ] Onboarding flow with state persistence
- [ ] Lesson card UI (word + image + TTS)
- [ ] Story renderer (formatted text)
- [ ] Progress bar component
- [ ] Text input with reflection prompt
- [ ] Audio player (expo-av)
- [ ] Offline mode indicator

#### Backend (Firebase)
- [ ] User profile schema (name, level, motivation)
- [ ] Lesson data schema (letters, words, pronunciations)
- [ ] Story schema (title, content, phonetics_used)
- [ ] Reflection submissions (user_id, lesson_id, text, timestamp)
- [ ] Progress tracking (letters_learned, stories_completed)
- [ ] Firestore security rules (read own data only)

#### TTS & Audio
- [ ] Set up Expo Speech (text-to-speech in Portuguese)
- [ ] Pre-record audio for letters (if TTS quality is poor)
- [ ] Cache audio files locally (expo-file-system)
- [ ] Test on low-bandwidth networks

#### Offline
- [ ] SQLite for local lesson cache
- [ ] Sync reflections when online
- [ ] Indicate sync status to user

---

## Phase 3: Polish & Testing (Weeks 5–6)

### QA
- [ ] Test on Android 11, 12, 13, 14
- [ ] Test on iOS 14, 15, 16
- [ ] Test offline: disable internet, verify lessons still load
- [ ] Test on slow networks (throttle to 2G)
- [ ] Crash reporting (Sentry)
- [ ] Performance profiling (slow screens)

### User Testing
- [ ] Session with Sr. Hélio or similar learner
- [ ] Observe: Can they navigate without text instructions?
- [ ] Collect: What's confusing? What motivates?
- [ ] Iterate: Fix top 3 issues

### Content Review
- [ ] Literacy expert: Do stories reflect reality?
- [ ] Pedagogy expert: Do reflections encourage conscientization?
- [ ] Audio: Is Portuguese clear for non-literate learners?

### Launch Prep
- [ ] Write app store listings (Apple, Google)
- [ ] Create screenshots + preview video
- [ ] Set up beta testing (TestFlight, Google Play Console)
- [ ] Prepare rollout plan

---

## Technology Stack Details

### React Native Setup
```bash
npx create-expo-app@latest alfabetizacao-app
cd alfabetizacao-app
npx expo install expo-av expo-file-system expo-speech expo-sqlite expo-dev-client
npm install firebase react-navigation @react-navigation/native @react-navigation/stack typescript @types/react-native
```

### Firebase Config
```javascript
// firebase.config.js
import { initializeApp } from 'firebase/app';
import { getAuth } from 'firebase/auth';
import { getFirestore } from 'firebase/firestore';
import { getStorage } from 'firebase/storage';

const firebaseConfig = {
  // env vars
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const db = getFirestore(app);
export const storage = getStorage(app);
```

### Folder Structure
```
alfabetizacao-app/
  src/
    screens/
      OnboardingScreen.tsx
      LessonScreen.tsx
      StoryScreen.tsx
      ProgressScreen.tsx
    components/
      WordCard.tsx
      ProgressBar.tsx
      Button.tsx
    services/
      firebase.ts
      tts.ts
      sync.ts
    data/
      lessons.json          # Letters A-J, words, phonetics
      stories.json          # Story texts
      reflections.json      # Sample prompts
    types/
      index.ts
    App.tsx
  app.json
  eas.json
  package.json
```

### Data Schema (Firestore)

```javascript
// users/{userId}
{
  id: string,
  name: string,
  motivation: string,
  createdAt: timestamp,
  lettersCompleted: string[], // ["A", "B", "C"]
  storiesRead: string[],
  lastActiveAt: timestamp,
}

// lessons/{lessonId}
{
  id: string,
  letter: string,
  phonetic: string, // IPA
  words: [
    {
      text: string,
      image: string (url),
      pronunciation: string,
    }
  ],
  audioUrl: string (TTS or pre-recorded),
}

// stories/{storyId}
{
  id: string,
  title: string,
  content: string,
  phoneticsUsed: string[], // ["A", "E", "I"]
  reflectionPrompt: string,
  difficulty: "easy" | "medium",
}

// reflections/{reflectionId}
{
  userId: string,
  lessonId: string,
  storyId: string,
  text: string,
  timestamp: timestamp,
}
```

---

## Release Checklist

### Before Beta
- [ ] All screens working offline
- [ ] TTS working in Portuguese
- [ ] No console warnings
- [ ] App icon + splash screen
- [ ] Privacy policy + terms of service
- [ ] Crash reporting enabled

### Before Public Launch
- [ ] 10+ beta testers (including Sr. Hélio-like personas)
- [ ] 95%+ daily retention (should be high for motivated learners)
- [ ] App store review (Apple guidelines: accessibility, no inappropriate content)
- [ ] Press kit: announcement, photos, story of Sr. Hélio

---

## Success Metrics (MVP)

- Session frequency: 5+ days/week
- Session length: 15–30 minutes
- Letters completed: 5+ out of 10
- Reflection rate: 80%+ of lessons result in reflection
- Retention @ day 7: 60%+
- Net Sentiment Score (NPS): +40 or higher

---

## Cost Breakdown

| Category | Cost | Notes |
|----------|------|-------|
| Design | $500–1000 | Figma + UI/UX review |
| Development | $3000–5000 | 4–6 weeks @ $750–850/week or in-house |
| Content | $600–1000 | Stories, phonics, illustrations, voice talent |
| Infrastructure | $100–200/mo | Firebase free tier + paid after $0/mo |
| Testing | $200–500 | User sessions, beta management |
| **Total** | **$4400–7700** | One-time + ~$100/mo ongoing |

---

## Timeline

| Week | Deliverable |
|------|------------|
| 1–2 | Design, content, tech setup |
| 3–4 | Core screens, Firebase integration |
| 5–6 | Testing, user feedback, launch prep |
| 7 | Beta launch (limited) |
| 8+ | Iterate, add letters K–Z, scale |

**Realistic MVP launch**: 6–8 weeks of focused work.
