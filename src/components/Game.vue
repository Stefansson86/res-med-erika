<template>
  <div class="game-container">
    <h1>På Spåret</h1>

    <div class="score-display">
      <p>Totalpoäng: {{ totalScore }}</p>
    </div>

    <div v-if="!hasWon" class="game-active">
      <div class="clue-section">
        <h2>Ledtråd {{ currentClueIndex + 1 }} av {{ currentDestination.clues.length }}</h2>
        <p class="clue-text">{{ currentClue.text }}</p>
        <p class="points-info">Värd: {{ currentClue.points }} poäng</p>
      </div>

      <div class="guess-section">
        <input
          v-model="currentGuess"
          @keyup.enter="submitGuess"
          type="text"
          placeholder="Gissa destination..."
          class="guess-input"
        />
        <button @click="submitGuess" class="submit-button">Gissa</button>
      </div>

      <div v-if="feedbackMessage" class="feedback">
        {{ feedbackMessage }}
      </div>
    </div>

    <div v-else class="win-section">
      <h2>🎉 Rätt!</h2>
      <p class="win-message">Vi är i <strong>{{ currentDestination.name }}</strong>.</p>
      <p class="win-points">Du fick <strong>{{ lastPoints }}</strong> poäng.</p>
      <button @click="nextDestination" class="next-button">Nästa destination</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { destinations } from '../data/destinations.js'

// State
const currentDestinationIndex = ref(0)
const currentClueIndex = ref(0)
const currentGuess = ref('')
const totalScore = ref(0)
const hasWon = ref(false)
const feedbackMessage = ref('')
const lastPoints = ref(0)

// Computed
const currentDestination = computed(() => destinations[currentDestinationIndex.value])
const currentClue = computed(() => currentDestination.value.clues[currentClueIndex.value])

// Methods
const submitGuess = () => {
  if (!currentGuess.value.trim()) {
    feedbackMessage.value = 'Skriv in en gissning!'
    return
  }

  const guess = currentGuess.value.trim().toLowerCase()
  const correctAnswer = currentDestination.value.name.toLowerCase()

  if (guess === correctAnswer) {
    // Rätt svar!
    lastPoints.value = currentClue.value.points
    totalScore.value += lastPoints.value
    hasWon.value = true
    feedbackMessage.value = ''
    currentGuess.value = ''
  } else {
    // Fel svar
    if (currentClueIndex.value < currentDestination.value.clues.length - 1) {
      // Det finns fler ledtrådar
      currentClueIndex.value++
      feedbackMessage.value = 'Tyvärr, fel svar. Här kommer nästa ledtråd.'
      currentGuess.value = ''
    } else {
      // Inga fler ledtrådar
      feedbackMessage.value = `Tyvärr, inga fler ledtrådar! Rätt svar var ${currentDestination.value.name}.`
      currentGuess.value = ''
    }
  }
}

const nextDestination = () => {
  // Återställ för nästa runda (funkar inte riktigt än eftersom vi bara har en destination)
  hasWon.value = false
  currentClueIndex.value = 0
  currentGuess.value = ''
  feedbackMessage.value = ''
  lastPoints.value = 0

  // Här skulle man byta till nästa destination om det fanns fler
  // currentDestinationIndex.value++
}
</script>

<style scoped>
.game-container {
  max-width: 600px;
  width: 90%;
  padding: 2rem;
  background: #f5f5f5;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  color: #2c3e50;
  margin-bottom: 1rem;
  font-size: 2.5rem;
}

.score-display {
  background: #fff;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 2rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.score-display p {
  font-size: 1.2rem;
  font-weight: bold;
  color: #3498db;
  margin: 0;
}

.clue-section {
  background: #fff;
  padding: 1.5rem;
  border-radius: 8px;
  margin-bottom: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.clue-section h2 {
  color: #2c3e50;
  margin-bottom: 1rem;
  font-size: 1.3rem;
}

.clue-text {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #34495e;
  margin-bottom: 0.5rem;
}

.points-info {
  color: #27ae60;
  font-weight: bold;
  margin-top: 0.5rem;
}

.guess-section {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.guess-input {
  flex: 1;
  padding: 0.75rem;
  font-size: 1rem;
  border: 2px solid #ddd;
  border-radius: 6px;
  outline: none;
  transition: border-color 0.3s;
}

.guess-input:focus {
  border-color: #3498db;
}

.submit-button {
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  font-weight: bold;
  color: #fff;
  background: #3498db;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.3s;
}

.submit-button:hover {
  background: #2980b9;
}

.feedback {
  background: #fff3cd;
  padding: 1rem;
  border-radius: 6px;
  color: #856404;
  font-weight: 500;
}

.win-section {
  background: #fff;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.win-section h2 {
  color: #27ae60;
  font-size: 2rem;
  margin-bottom: 1rem;
}

.win-message {
  font-size: 1.3rem;
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.win-points {
  font-size: 1.2rem;
  color: #27ae60;
  margin-bottom: 1.5rem;
}

.next-button {
  padding: 0.75rem 2rem;
  font-size: 1.1rem;
  font-weight: bold;
  color: #fff;
  background: #27ae60;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.3s;
}

.next-button:hover {
  background: #229954;
}
</style>
