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

1. Bygg projektet: `npm run build`
2. Pusha dist-mappen till gh-pages-branchen
3. Aktivera GitHub Pages i repository settings

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
