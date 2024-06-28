<script setup>
import { ref, onMounted } from 'vue'

const advice = ref({})
const loading = ref(false)
const fetchAdvice = async () => {
  loading.value = true
  const res = await fetch('https://api.adviceslip.com/advice')
  const data = await res.json()
  advice.value = data.slip
  loading.value = false
}

onMounted(() => fetchAdvice())
</script>

<template>
  <div class="card" :class="{ loading }">
    <h1 class="advice-id">advice #{{ advice?.id }}</h1>
    <blockquote>
      <p class="advice">
        {{ `"${advice?.advice}"` }}
      </p>
    </blockquote>
    <picture>
      <img class="divider" srcset="/images/pattern-divider-mobile.svg 295w, /images/pattern-divider-desktop.svg 444w"
        sizes="(max-width: 518px) 295px, 444px" src="/images/pattern-divider-mobile.svg" alt="divider">
    </picture>
    <button @click="fetchAdvice" class="get-advice-btn" aria-label="click to generate advice">
      <img src="/images/icon-dice.svg" alt="dice icon">
    </button>
  </div>
</template>

<style scoped>
.card {
  width: 100%;
  background-color: var(--Dark-grayish-blue);
  border-radius: 1rem;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  position: relative;
}

.advice-id {
  color: var(--Neon-green);
  text-transform: uppercase;
  letter-spacing: 3px;
  font-size: 0.8rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.advice {
  color: var(--Light-cyan);
  font-size: 28px;
  font-weight: 800;
  text-align: center;
  margin-bottom: 0.5rem;
}

.divider {
  padding-bottom: 2rem;
}

.get-advice-btn {
  background-color: var(--Neon-green);
  border: none;
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  position: absolute;
  bottom: -2rem;
  box-shadow: none;
  transition: 0.1s ease-in-out;
}

.get-advice-btn:hover {
  box-shadow: 0 0 2.5rem var(--Neon-green);
  transition: 0.25s ease-in-out;
}

.get-advice-btn:active {
  outline: none;
  box-shadow: none;
}

.card.loading>button>img {
  animation: rotate 0.6s infinite ease-in;
}

.card.loading {

  h1,
  blockquote,
  picture {
    visibility: hidden;
  }
}

.card.loading {
  background-image: linear-gradient(235deg, var(--Dark-blue), var(--Grayish-blue), var(--Dark-blue));
  background-size: 200% 200%;
  animation: slide 2s infinite linear;
}

@-webkit-keyframes slide {
  0% {
    background-position: 0% 81%
  }

  50% {
    background-position: 100% 20%
  }

  100% {
    background-position: 0% 81%
  }
}

@-moz-keyframes slide {
  0% {
    background-position: 0% 81%
  }

  50% {
    background-position: 100% 20%
  }

  100% {
    background-position: 0% 81%
  }
}

@keyframes slide {
  0% {
    background-position: 0% 81%
  }

  50% {
    background-position: 100% 20%
  }

  100% {
    background-position: 0% 81%
  }
}

@-webkit-keyframes rotate {
  to {
    transform: rotate(360deg);
  }
}

@-moz-keyframes rotate {
  to {
    transform: rotate(360deg);
  }
}

@keyframes rotate {
  to {
    transform: rotate(360deg);
  }
}

@media screen and (width >=580px) {
  .card {
    max-width: 518px;
  }
}
</style>
