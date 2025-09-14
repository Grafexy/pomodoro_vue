<script setup lang="ts">
import { ref, computed, onUnmounted } from 'vue'

// Timer state
const minutes = ref(25) // Default pomodoro time
const seconds = ref(0)
const isActive = ref(false)
const isBreak = ref(false)
const sessionCount = ref(0)

let interval: number | null = null

// Computed properties
const displayTime = computed(() => {
  const m = minutes.value.toString().padStart(2, '0')
  const s = seconds.value.toString().padStart(2, '0')
  return `${m}:${s}`
})

const progressPercentage = computed(() => {
  const totalTime = isBreak.value ? 5 * 60 : 25 * 60 // 5 min break, 25 min work
  const currentTime = minutes.value * 60 + seconds.value
  return ((totalTime - currentTime) / totalTime) * 100
})

// Timer functions
function startTimer() {
  if (isActive.value) {
    pauseTimer()
    return
  }

  isActive.value = true
  interval = setInterval(() => {
    if (seconds.value > 0) {
      seconds.value--
    } else if (minutes.value > 0) {
      minutes.value--
      seconds.value = 59
    } else {
      // Timer finished
      completeSession()
    }
  }, 1000)
}

function pauseTimer() {
  isActive.value = false
  if (interval) {
    clearInterval(interval)
    interval = null
  }
}

function resetTimer() {
  pauseTimer()
  if (isBreak.value) {
    minutes.value = 5
    seconds.value = 0
  } else {
    minutes.value = 25
    seconds.value = 0
  }
}

function completeSession() {
  pauseTimer()

  if (!isBreak.value) {
    sessionCount.value++
    isBreak.value = true
    minutes.value = 5
    seconds.value = 0
  } else {
    isBreak.value = false
    minutes.value = 25
    seconds.value = 0
  }

  // Play notification sound (browser beep)
  if ('AudioContext' in window) {
    const audioCtx = new AudioContext()
    const oscillator = audioCtx.createOscillator()
    const gainNode = audioCtx.createGain()

    oscillator.connect(gainNode)
    gainNode.connect(audioCtx.destination)

    oscillator.frequency.value = 800
    gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime)
    oscillator.start()
    oscillator.stop(audioCtx.currentTime + 0.5)
  }
}

// Cleanup on unmount
onUnmounted(() => {
  if (interval) {
    clearInterval(interval)
  }
})
</script>

<template>
  <div class="pomodoro-timer">
    <h1>🍅 Pomodoro Timer</h1>

    <div class="timer-circle">
      <svg width="300" height="300" class="progress-ring">
        <circle cx="150" cy="150" r="120" stroke="#e6e6e6" stroke-width="8" fill="none" />
        <circle
          cx="150"
          cy="150"
          r="120"
          stroke="#ff6b6b"
          stroke-width="8"
          fill="none"
          :stroke-dasharray="`${2 * Math.PI * 120}`"
          :stroke-dashoffset="`${2 * Math.PI * 120 * (1 - progressPercentage / 100)}`"
          class="progress-circle"
        />
      </svg>

      <div class="timer-content">
        <div class="time-display">{{ displayTime }}</div>
        <div class="session-type">
          {{ isBreak ? 'Break Time' : 'Focus Time' }}
        </div>
        <div class="session-count">Sessions: {{ sessionCount }}</div>
      </div>
    </div>

    <div class="controls">
      <button @click="startTimer" class="btn btn-primary">
        {{ isActive ? 'Pause' : 'Start' }}
      </button>
      <button @click="resetTimer" class="btn btn-secondary">Reset</button>
    </div>
  </div>
</template>

<style scoped>
.pomodoro-timer {
  text-align: center;
  padding: 2rem;
  max-width: 600px;
  margin: 0 auto;
}

h1 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #333;
}

.timer-circle {
  position: relative;
  display: inline-block;
  margin-bottom: 2rem;
}

.progress-ring {
  transform: rotate(-90deg);
}

.progress-circle {
  transition: stroke-dashoffset 1s linear;
}

.timer-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
}

.time-display {
  font-size: 3rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 0.5rem;
}

.session-type {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 0.5rem;
}

.session-count {
  font-size: 1rem;
  color: #888;
}

.controls {
  display: flex;
  gap: 1rem;
  justify-content: center;
}

.btn {
  padding: 0.75rem 1.5rem;
  font-size: 1.1rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 600;
}

.btn-primary {
  background-color: #ff6b6b;
  color: white;
}

.btn-primary:hover {
  background-color: #ff5252;
  transform: translateY(-2px);
}

.btn-secondary {
  background-color: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background-color: #5a6268;
  transform: translateY(-2px);
}

.btn:active {
  transform: translateY(0);
}

@media (max-width: 768px) {
  .timer-circle {
    transform: scale(0.8);
  }

  .time-display {
    font-size: 2.5rem;
  }

  h1 {
    font-size: 2rem;
  }
}
</style>
