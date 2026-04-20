# Caminho das Letras — Local Project Setup

## What's Here

This folder contains the initial concept, MVP definition, and structure for **Caminho das Letras** — an adult literacy app inspired by Paulo Freire's pedagogy.

### Documentation

- **PROJECT_VISION.md** — Full vision, pedagogy, target persona (Sr. Hélio), why this matters
- **MVP_BREAKDOWN.md** — Technical roadmap, screens, implementation checklist, timeline
- **PEDAGOGYY_NOTES.md** — Deep dive into Paulo Freire's approach and how we apply it
- **CONTENT_PIPELINE.md** — How to write and test stories and phonetic lessons
- **TEAM_AND_ROLES.md** — Who owns what (for when we grow)

### Folder Structure (when repo is initialized)

```
alfabetizacao-app/
  docs/
    PROJECT_VISION.md
    MVP_BREAKDOWN.md
    PEDAGOGY_NOTES.md
    CONTENT_PIPELINE.md
    TEAM_AND_ROLES.md
  app/                          # React Native app (Expo)
    src/
      screens/
      components/
      services/
      data/
      types/
    app.json
    eas.json
    package.json
  content/                      # Stories, phonics data, reflections
    stories/
      pt_BR/
        o-dia-de-helio.md
        carta-para-mae.md
    phonetics/
      letters-a-j.json
    prompts/
      reflections.json
  scripts/
    seed-lessons.ts             # Load content into Firebase
    export-data.ts              # Export user data for research
  .github/
    workflows/
      test.yml                  # Run tests on PR
      build.yml                 # EAS build on release
  .gitignore
  README.md
```

---

## Getting Started (when repo is live)

### Prerequisites
- Node.js 18+
- React Native / Expo CLI
- Firebase account
- GitHub account (ofundefined org)

### Local Setup
```bash
git clone https://github.com/ofundefined/alfabetizacao-app.git
cd alfabetizacao-app/app
npm install
npx expo start
```

### Firebase Setup
```bash
# Create .env.local with your Firebase config
EXPO_PUBLIC_FIREBASE_API_KEY=...
EXPO_PUBLIC_FIREBASE_PROJECT_ID=...
# etc
```

### Run on Device
```bash
# Start Expo dev server
npx expo start

# Open on Android device or iOS
# (scan QR code or press 'i' for iOS simulator)
```

---

## MVP Phases

1. **Weeks 1–2**: Design + setup
2. **Weeks 3–4**: Core features (onboarding, 1 letter, 1 story)
3. **Weeks 5–6**: Testing, user feedback, launch prep
4. **Week 7+**: Beta launch, iterate, expand to all 10 letters

---

## Key Decisions

| Decision | Rationale |
|----------|-----------|
| React Native (Expo) | Cross-platform, rapid iteration, offline-first support |
| Firebase | Quick launch, scales with users, free tier generous |
| Portuguese only (MVP) | Focus on depth, not breadth |
| Offline-first | Rural connectivity is unpredictable |
| Reflection prompts | Freire's conscientization — user agency matters |
| Simple visual design | Large text, high contrast, low cognitive load |

---

## Next Steps (Before Coding)

1. **[GitHub]** Create repo in ofundefined org: `alfabetizacao-app`
2. **[Content]** Interview Sr. Hélio or similar learner: What do you want to read?
3. **[Design]** Sketch wireframes in Figma (key screens)
4. **[Content]** Draft 2 stories with real-world context
5. **[Tech]** Set up Firebase project and EAS (Expo build service)

---

## People Involved

- **Concept & Pedagogy**: You (leading Freiriano approach)
- **Development**: React Native expert (you or team)
- **Content**: Literacy specialist + community voices
- **User Research**: Sr. Hélio + similar learners

---

## Resources

- [Paulo Freire — Pedagogy of the Oppressed](https://en.wikipedia.org/wiki/Pedagogy_of_the_Oppressed)
- [Expo Documentation](https://docs.expo.dev/)
- [Firebase + React Native](https://rnfirebase.io/)
- [Adult Literacy in Brazil (ABCD Method)](https://www.nlm.nih.gov/pubmed/1604435)
- [Duolingo Case Study](https://blog.duolingo.com/how-duolingo-built-engagement/) (what to learn from, not copy)

---

## Questions to Answer Before Launch

- **Budget**: How much can we invest in MVP?
- **Team**: Who leads content? Who builds?
- **Timeline**: What's the deadline?
- **Users**: How do we find Sr. Hélio and others to test with?
- **Sustainability**: After launch, how do we fund ongoing support?
- **Language**: Portuguese only, or eventually Spanish, other languages?

---

## License & Ethics

This project is inspired by Paulo Freire's work and the principle that **literacy is a human right, not a luxury**.

All content and code will be open-source (likely MIT or CC-BY-SA) to enable other communities to adapt and use it.

We commit to:
- Never charging for this app (free for all)
- Respecting user privacy (no ads, no data sales)
- Centering the voices of learners (not experts dictating)
- Community-driven content (co-created with Sr. Hélio and others)
