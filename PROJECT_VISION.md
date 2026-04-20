# Caminho das Letras (Path of Letters)

> An adult literacy app inspired by Paulo Freire's pedagogy for rural workers and underserved communities.

## Vision

Empower Sr. Hélio and millions like him — adults who never learned to read despite decades of work and life experience — to reclaim literacy with dignity, cultural relevance, and joy.

**Freiriano approach**: Literacy is not just decoding text. It's critical consciousness-raising. Learners see their own world reflected in lessons: rural labor, family, dignity, survival, hope.

## Target Persona

**Sr. Hélio**
- Age: 50+
- Background: Rural worker ("roça"), daily wage labor in agriculture
- Never attended school or dropped out early
- Has oral knowledge, practical wisdom, dignity
- Wants to read contracts, letters from family, instructions
- Uses smartphone (increasingly common in rural BR)
- Low education confidence but high life wisdom

Similar personas: domestic workers, security guards, construction workers, anyone who grew up in poverty with no schooling.

## Why "Caminho das Letras"?

- "Caminho" = path, journey (not a race like Duolingo)
- "Letras" = letters, writing, literature
- Honors the idea of walking, accumulation, dignity
- Cultural resonance in Portuguese

Alternative names considered:
- **Semente da Leitura** (Literacy Seed) — emphasizes growth
- **Voz do Hélio** (Hélio's Voice) — personal, specific
- **Alfabeto da Vida** (Life's Alphabet) — holistic

---

## Key Differences from Duolingo

| Duolingo | Caminho das Letras |
|----------|-------------------|
| Fast, gamified, streaks | Paced, reflective, community-oriented |
| Abstract sentences | Real-world contexts: labor, family, documents |
| Competitive points | Collective stories, shared recognition |
| Multiple languages | Monolingual (Portuguese), deep phonics |
| Young learners image | Explicit elder/adult imagery and respect |
| Vocabulary → Grammar | Phonics → Word families → Sentences → Stories |

---

## Core Pedagogy (Paulo Freire)

1. **Conscientization**: Learners reflect on their reality and agency
2. **Problem-posing**: Lessons ask questions, don't just deliver answers
3. **Cultural relevance**: Stories from their world (harvest, family, dignity)
4. **Community**: Learning together, not alone chasing points
5. **Empowerment**: Literacy as tool for voice, not just skill

Example lesson frame:
- **Theme**: "Entendendo o contrato de trabalho" (Understanding a work contract)
- **Lived experience**: "Você já assinou algo sem entender?" (Have you ever signed without understanding?)
- **Decode**: Learn key words: "salário", "horário", "responsabilidade"
- **Reflect**: "Por que é importante ler um contrato?" (Why does this matter?)
- **Action**: Take a photo of a real contract, practice reading parts aloud

---

## Tech Stack

- **Frontend**: React Native (Expo) — cross-platform, rapid iteration
- **Backend**: Node.js + Express (or Firebase for MVP)
- **Database**: PostgreSQL (for scalability) or Firebase Firestore (for speed)
- **Auth**: Simple email/phone code
- **Sync**: Offline-first for rural connectivity (limited internet)
- **Analytics**: Plausible or PostHog (respect privacy)
- **CI/CD**: GitHub Actions → EAS Build (Expo)
- **Hosting**: Vercel (web) + EAS Hosted (mobile app distribution)

---

## MVP Scope (4–6 weeks)

### Must Have (P0)
- [ ] Onboarding flow (name, age, motivation, context)
- [ ] Phonics progression: 10 letters (A–J)
- [ ] Word family introduction: 5 simple words per letter (e.g., "A: ato, abre, avó")
- [ ] One simple story: "O Dia de Hélio" (Hélio's Day) — 50 words, uses learned letters
- [ ] Read-aloud: tap words for pronunciation (TTS)
- [ ] Progress tracking: visual bar showing letters learned
- [ ] Offline mode: lesson content cached locally
- [ ] One reflection prompt per lesson ("Como você se sente?")

### Should Have (P1)
- [ ] Spaced repetition: review reminders (3 days, 7 days, 14 days)
- [ ] Earn simple badges (unlocked, not gated)
- [ ] Glossary: tap word → simple definition + image
- [ ] Parent/mentor mode: track learner progress (for literacy volunteers)

### Won't Have (out of scope for MVP)
- Multiple languages
- Video animations (just static + TTS for now)
- Social features
- Backend API (Firebase for rapid dev)
- Adaptive difficulty

---

## User Journey (MVP)

```
Start App
  ↓
Onboarding (name, motivation)
  ↓
Letter A: Learn phoneme + 5 words
  ↓
Story time: Read "O Dia de Hélio" (uses Letter A words)
  ↓
Reflection: "How did that feel?"
  ↓
Letter B (repeat pattern)
  ↓
Progress dashboard: "You've learned A, B, C..."
  ↓
Review lesson (spaced repetition)
  ↓
[Repeat for Letters C–J]
```

---

## Metrics to Track

- Sessions per day / daily active users
- Time in app per session
- Letters completed
- Story completion rate
- Reflection responses (sentiment)
- Offline usage rate
- Retention @ 3 days, 7 days, 30 days

---

## Content Creation (MVP Stories)

1. **"O Dia de Hélio"** (The Day of Hélio)
   - ~50 words
   - Uses A–E phonetics
   - Daily rural labor context
   - Reflection: "Você também trabalha? Fale sobre seu dia."

2. **"Carta para Mãe"** (Letter to Mom)
   - ~60 words
   - Uses F–J phonetics
   - Family context
   - Reflection: "A quem você gostaria de escrever?"

---

## Team & Roles (for later phases)

- **Product Lead**: Define pedagogy + user research
- **React Native Dev**: App development (frontend)
- **Backend Dev**: API, data persistence
- **Content Creator**: Write stories, phonics lessons (needs literacy expert)
- **Paulo Freire Scholar**: Ensure pedagogy aligns with conscientization principles
- **Community Manager**: Collect feedback from Sr. Hélio and similar learners

---

## Success Criteria (MVP)

- [ ] 5+ test users complete at least 3 letters
- [ ] Average session time > 10 minutes
- [ ] No crashes on Android 11+ and iOS 14+
- [ ] Offline mode works: lesson loads without internet
- [ ] TTS works reliably in Portuguese
- [ ] Reflection prompts generate thoughtful responses
- [ ] Battery usage < 50MB per 30-min session

---

## Next Steps

1. **Design**: Sketch UI mockups (Figma) — simple, large text, high contrast
2. **Content**: Write and test 2 stories with literacy experts
3. **Prototype**: Build React Native scaffold with onboarding + 1 letter
4. **User testing**: Sit with Sr. Hélio, watch them use it, iterate
5. **Expand**: Add letters B–J, more stories, spaced repetition
6. **Launch**: Internal beta with 10–20 rural volunteer learners
7. **Scale**: Community partnerships (NGOs, adult ed centers)

---

## Budget Estimate (MVP)

- Design (wireframes + mockups): $500–1000
- Development (React Native + Firebase setup): $2000–4000 (agency) or 4–6 weeks (in-house)
- Content (2 stories, phonics sequences, illustrations): $500–800
- Testing + user research: $300–500
- Infrastructure (Firebase free tier, EAS Build credits): ~$100/mo

**Total MVP**: $3500–7300

---

## Inspiration & References

- **Paulo Freire**: "Pedagogy of the Oppressed" — critical literacy
- **Duolingo**: Engagement mechanics (not pedagogy)
- **Libby.ai**: Audio + text for literacy
- **Room to Read**: Global literacy initiatives
- **ABCD Method**: Adult literacy in Brazil (proven)
