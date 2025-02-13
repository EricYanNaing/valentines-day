<script setup>
import { ref, onMounted } from 'vue'
import { DotLottieVue } from '@lottiefiles/dotlottie-vue'

const showThankYou = ref(false)
const showModal = ref(false)
const response = ref('')
const name = ref('')
const noClickCount = ref(0) // Counter for "No" button clicks
const noButtonVisible = ref(true) // Control button visibility
const noButtonStyle = ref({
  position: 'relative',
  left: '0px',
  top: '0px',
})

const handleResponse = (answer) => {
  if (answer === 'yes') {
    showModal.value = true
  } else {
    response.value = answer
    showThankYou.value = true
  }
}

// Function to randomly move the "No" button
const moveNoButton = () => {
  if (!noButtonVisible.value) return

  noClickCount.value++
  if (noClickCount.value >= 5) {
    noButtonVisible.value = false // Hide the "No" button after 5 clicks
    return
  }

  const randomX = Math.random() * 200 - 100 // Moves randomly left or right
  const randomY = Math.random() * 200 - 100 // Moves randomly up or down

  noButtonStyle.value = {
    position: 'relative',
    left: `${randomX}px`,
    top: `${randomY}px`,
    transition: 'left 0.2s ease, top 0.2s ease',
  }
}

const closeModal = () => {
  showModal.value = false
}

const submitForm = () => {
  alert(`Thank you, ${name.value}! You are my Valentine! ❤️`)
  showModal.value = false
}

onMounted(() => {
  import('@lottiefiles/lottie-player')
})
</script>

<template>
  <div class="min-h-screen flex flex-col relative">
    <!-- Background Lottie -->
    <div class="fixed inset-0 -z-10">
      <DotLottieVue 
        class="w-full h-full" 
        autoplay 
        loop 
        src="https://lottie.host/875dda11-d211-4c6b-9dae-bea59764ef05/OyeEtI147R.lottie" 
      />
    </div>

    <a href="https://github.com/EricYanNaing/valentines-day" target="_blank">
      <DotLottieVue 
        class="w-10 h-10 github" 
        autoplay 
        loop 
        src="https://lottie.host/e176a65b-dd66-43bd-9a2d-3ea5d27d759c/fHcvQHHS4j.lottie" 
      />
    </a>

    <!-- Logo Section -->
    <header class="w-full max-w-md mx-auto pt-8">
      <DotLottieVue 
        class="w-full h-64" 
        autoplay 
        loop 
        src="https://lottie.host/aa713ff9-82c2-48ab-95e5-00722f3af0ce/asaA25ZDLF.lottie" 
      />
    </header>

    <!-- Main Content -->
    <main class="w-full max-w-md mx-auto p-3">
      <p class="text-3xl font-semibold mt-4 romantic-text p-4 text-center">
          " Will you be my valentines 💖 ? "
        </p>
    </main>

    <!-- Footer with Buttons -->
    <footer class="w-full py-8 px-4">
      <div v-if="!showThankYou" class="flex justify-center gap-4">
        <button 
          @click="handleResponse('yes')"
          class="bg-violet-500  flex items-center hover:bg-violet-600 text-white font-bold py-3 px-8 rounded-full transition-colors"
        >
        <span class="material-icons text-white">favorite</span>
          Yes
        </button>
        <button 
          v-if="noButtonVisible"
          @click.prevent="moveNoButton"
          class="bg-red-500 text-white font-bold py-3 px-8 rounded-full transition-colors"
          :style="noButtonStyle"
        >
          No
        </button>
      </div>
      <div v-else class="text-center">
        <p class="text-2xl font-bold text-white">
          Thank you for your response: {{ response }}!
        </p>
      </div>
    </footer>

    <!-- Modal -->
    <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center p-4">
      <div class="bg-white p-6 rounded-lg shadow-lg max-w-md w-full text-center">
        <!-- Lottie Animation -->
        <DotLottieVue 
          class="w-full h-full mx-auto" 
          autoplay 
          src="https://lottie.host/42af5c7b-873f-4216-acde-c50ded5efd9e/wyVNMha0jC.lottie" 
        />

        <!-- Romantic Message -->
        <p class="text-lg font-semibold mt-4 romantic-text">
          "You just made my heart dance! 💖 Thank you for saying yes! 
          I will remember this most special Valentine ever!"
        </p>

        
        <!-- Buttons -->
        <div class="flex justify-center mt-4">
          <button 
            @click="closeModal" 
            class="bg-violet-500 flex items-center hover:bg-violet-600 text-white py-2 px-4 rounded-2xl"
          >
            <span class="material-icons text-white">favorite</span>
            
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
