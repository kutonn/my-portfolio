<template>
  <Transition name="modal">
    <div v-if="selectedProject" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <!-- Header -->
        <div class="modal-header">
          <h2>{{ selectedProject.title }}</h2>
          <button class="close-btn" @click="closeModal">
            <i class="fas fa-times"></i>
          </button>
        </div>

        <!-- Screenshot Slideshow -->
        <div class="slideshow-container">
          <div class="slideshow-wrapper">
            <img 
              v-for="(screenshot, index) in selectedProject.screenshots"
              :key="index"
              :src="screenshot"
              :alt="`${selectedProject.title} screenshot ${index + 1}`"
              class="slideshow-image"
              :class="{ active: currentSlide === index }"
              @click="nextSlide"
            >
          </div>
          
          <!-- Slide Indicators -->
          <div class="slide-indicators">
            <button 
              v-for="(screenshot, index) in selectedProject.screenshots"
              :key="index"
              class="indicator"
              :class="{ active: currentSlide === index }"
              @click="currentSlide = index"
            ></button>
          </div>
          
          <!-- Navigation Arrows -->
          <button class="nav-arrow prev" @click="prevSlide">
            <i class="fas fa-chevron-left"></i>
          </button>
          <button class="nav-arrow next" @click="nextSlide">
            <i class="fas fa-chevron-right"></i>
          </button>
        </div>

        <!-- Project Details -->
        <div class="project-details">
          <div class="tech-stack">
            <span v-for="tech in selectedProject.tech" :key="tech" class="tech-tag">
              {{ tech }}
            </span>
          </div>
          <p>{{ selectedProject.description }}</p>
          
          <!-- Action Buttons -->
          <div class="action-buttons">
            <a 
            v-if="selectedProject.liveDemo"
            :href="selectedProject.liveDemo"
            target="_blank"
            @click.stop
            class="btn-live"
            >
            {{ selectedProject.liveLabel || 'Live Demo' }}
          </a>
          <a 
            v-if="selectedProject.github"
            :href="selectedProject.github"
            target="_blank"
            @click.stop
            class="btn-code"
          >
            {{ selectedProject.codeLabel || 'View Code' }}
          </a>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  selectedProject: Object
})

const emit = defineEmits(['close'])

const currentSlide = ref(0)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % props.selectedProject.screenshots.length
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + props.selectedProject.screenshots.length) % props.selectedProject.screenshots.length
}

const closeModal = () => emit('close')

// Keyboard navigation
onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})

const handleKeydown = (e) => {
  if (e.key === 'ArrowRight') nextSlide()
  if (e.key === 'ArrowLeft') prevSlide()
  if (e.key === 'Escape') closeModal()
}
</script>

<style scoped>
.modal-enter-active, .modal-leave-active {
  transition: all 0.3s ease;
}
.modal-enter-from, .modal-leave-to {
  opacity: 0;
  transform: scale(0.95);
}

.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.9);
  backdrop-filter: blur(15px);
  z-index: 10000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}

.modal-content {
  background: white;
  border-radius: 24px;
  max-width: 1000px;
  max-height: 90vh;
  width: 100%;
  max-width: 90vw;
  overflow: hidden;
  box-shadow: 0 50px 100px rgba(0, 0, 0, 0.5);
  animation: modalSlideIn 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

@keyframes modalSlideIn {
  from {
    opacity: 0;
    transform: scale(0.8) translateY(50px);
  }
  to {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

.modal-header {
  padding: 2rem 2.5rem 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #f1f5f9;
}

.modal-header h2 {
  font-size: 2rem;
  font-weight: 700;
  color: #1f2937;
}

.close-btn {
  background: #f3f4f6;
  border: none;
  width: 44px;
  height: 44px;
  border-radius: 12px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  color: #6b7280;
  transition: all 0.3s ease;
}

.close-btn:hover {
  background: #fee2e2;
  color: #dc2626;
}

.slideshow-container {
  position: relative;
  height: 450px;
  overflow: hidden;
}

.slideshow-wrapper {
  height: 100%;
  position: relative;
}

.slideshow-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transition: opacity 0.6s ease;
  cursor: pointer;
}

.slideshow-image.active {
  opacity: 1;
}

.slide-indicators {
  position: absolute;
  bottom: 25px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 12px;
}

.indicator {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.indicator.active,
.indicator:hover {
  background: #2563eb;
  transform: scale(1.3);
}

.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.9);
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  color: #374151;
  transition: all 0.3s ease;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}

.nav-arrow:hover {
  background: white;
  transform: translateY(-50%) scale(1.1);
}

.prev { left: 20px; }
.next { right: 20px; }

.project-details {
  padding: 2.5rem;
}

.tech-stack {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.tech-tag {
  background: linear-gradient(135deg, #eff6ff, #dbeafe);
  color: #2563eb;
  padding: 0.5rem 1.25rem;
  border-radius: 25px;
  font-size: 0.9rem;
  font-weight: 600;
}

.project-details p {
  color: #64748b;
  line-height: 1.7;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.action-buttons {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.btn {
  flex: 1;
  min-width: 180px;
  padding: 1.1rem 2rem;
  border-radius: 16px;
  text-decoration: none;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 1rem;
}

.btn-primary {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  color: white;
  box-shadow: 0 10px 30px rgba(37, 99, 235, 0.4);
}

.btn-secondary {
  background: linear-gradient(135deg, #6b7280, #374151);
  color: white;
  box-shadow: 0 10px 30px rgba(107, 114, 128, 0.4);
}

.btn:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.btn-live, .btn-code {
  flex: 1;
  padding: 0.75rem;
  text-decoration: none;
  text-align: center;
  border-radius: 10px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-live {
  background: linear-gradient(135deg, #10b981, #059669);
  color: white;
}

.btn-code {
  background: #374151;
  color: white;
}


</style>