# På Spåret - Textbaserat Spel

Ett enkelt textbaserat På Spåret-spel byggt med Vue 3 och Vite.

## Installation

```bash
npm install
```

## Utveckling

Kör utvecklingsservern:

```bash
npm run dev
```

## Bygga för produktion

```bash
npm run build
```

## Deploya till GitHub Pages

Projektet använder GitHub Actions för automatisk deployment:

1. Gå till repository Settings → Pages
2. Under "Build and deployment", välj "GitHub Actions" som källa
3. Pusha till main/master branch - deployment sker automatiskt!
4. Spelet blir tillgängligt på: `https://stefansson86.github.io/res-med-erika/`

Eller kör workflow manuellt:
- Gå till "Actions" tab → "Deploy to GitHub Pages" → "Run workflow"

## Spelregler

- Spelet visar ledtrådar en i taget
- Gissa destinationen i textfältet
- Fel svar → nästa ledtråd visas
- Rätt svar → få poäng baserat på vilken ledtråd du klarade det på:
  - Ledtråd 1: 10 poäng
  - Ledtråd 2: 8 poäng
  - Ledtråd 3: 6 poäng
  - Ledtråd 4: 4 poäng
  - Ledtråd 5: 2 poäng

## Struktur

```
src/
├── main.js              # Applikationens startpunkt
├── App.vue              # Huvudkomponent
├── components/
│   └── Game.vue         # Spellogik och UI
└── data/
    └── destinations.js  # Destinationer och ledtrådar
```

## Lägg till fler destinationer

Redigera `src/data/destinations.js` och lägg till fler objekt i `destinations`-arrayen.
