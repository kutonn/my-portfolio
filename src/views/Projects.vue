<template>
  <section class="stats-section">
    <div class="container">
      
      <!-- Header -->
      <div class="section-header">
        <h2 class="section-title-1">Featured Projects</h2>
        <p class="section-subtitle">
          Handpicked projects showcasing my skills in Layout Design and Simple Web Development
        </p>
      </div>

      <!-- Filters -->
      <div class="projects-filters">
        <button 
          v-for="filter in filters" 
          :key="filter.value"
          class="filter-btn"
          :class="{ active: activeFilter === filter.value }"
          @click="setFilter(filter.value)"
        >
          <i :class="filter.icon"></i>
          {{ filter.label }}
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="projects-grid">
        <ProjectCard
        v-for="project in filteredProjects"
        :key="project.id"
        :project="project"
        @click="() => openProjectModal(project)"/>
      </div>
    </div>

    <!-- Modal -->
    <ProjectModal 
      v-if="showModal"
      :selected-project="selectedProject"
      @close="closeModal"
    />
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import ProjectCard from '../components/ProjectCard.vue'
import ProjectModal from '../components/ProjectModal.vue'

// ✅ CLEAN + CONSISTENT DATA
const projects = ref([
  {
    id: 1,
    title: 'Portfolio Website',
    description: 'This very portfolio! Built with Vue 3.',
    image: '/images/project1.png',
    tech: ['Vue 3', 'Vite', 'CSS3'],
    categories: ['web', 'design'],
    liveDemo: 'https://your-live-link.com',
    github: 'https://github.com/kutonn/my-portfolio.git',
    screenshots: [
    '/public/pweb1.png',
    '/public/pweb2.png',
    '/public/pweb3.png',
    '/public/pweb4.png'
    ]
  },
  {
    id: 2,
    title: 'PubMats',
    description: 'Layout Designs tailored for clients.',
    image: '/images/project2.png',
    tech: ['Canva', 'Photoshop'],
    categories: ['design'],
    liveDemo: 'https://canva.link/cknyjcoaot5f6af',
    github: null,
    liveLabel: 'View Designs',
    codeLabel: null,
    screenshots: [
      '/public/project1.png', 
      '/public/project2.png', 
      '/public/project3.png',
      '/public/project4.png',
      '/public/project5.png',
      '/public/project6.png',
      '/public/project7.png',
    ]
  },
  {
    id: 3,
    title: 'SwiftThreads Website',
    description: 'A school project that showcases a properly structured Cart, but with the limitation of a Database that stores User Information.',
    image: '/images/project3.png',
    tech: ['HTML', 'CSS'],
    categories: ['web', "mobile"],
    liveDemo: 'https://your-live-link.com',
    github: 'https://github.com/kutonn/Website.git',
    screenshots: [
      '/public/swift1.png',
      '/public/swift2.png',
      '/public/swift3.png',
      '/public/swift4.png',
      '/public/swift5.png',
    ]
  },
  {
    id: 4,
    title: 'Login and Register',
    description: 'A simple school project that showcases just a mere frontend only of a login and register page.',
    image: '/images/project3.png',
    tech: ['HTML', 'CSS'],
    categories: ['web', 'mobile'],
    liveDemo: 'https://your-live-link.com',
    github: 'https://github.com/kutonn/LoginReg.git',
    screenshots: [
      '/public/lr1.png',
      '/public/lr2.png',
      '/public/lr3.png',
      '/public/lr4.png',
      '/public/lr5.png',
      '/public/lr6.png',
      '/public/lr7.png',
    ]
  },
  {
    id: 6,
    title: 'Prototype Portfolio',
    description: 'A prototype version of this very portfolio.',
    image: '/images/project3.png',
    tech: ['HTML', 'CSS'],
    categories: ['web', 'design'],
    liveDemo: 'https://your-live-link.com',
    github: 'https://github.com/kutonn/Prototype-Portfolio.git',
    screenshots: [
      '/public/proto1.png',
      '/public/proto2.png',
      '/public/proto3.png',
      '/public/proto4.png',
      '/public/proto5.png',
      '/public/proto6.png',
      '/public/proto7.png',
      '/public/proto8.png',
    ]
  }
])

// State
const activeFilter = ref('all')
const showModal = ref(false)
const selectedProject = ref(null)

// Filters
const filters = [
  { label: 'All', value: 'all', icon: 'fas fa-th' },
  { label: 'Web', value: 'web', icon: 'fas fa-globe' },
  { label: 'Mobile', value: 'mobile', icon: 'fas fa-mobile-alt' },
  { label: 'Design', value: 'design', icon: 'fas fa-palette' }
]

// Methods
const setFilter = (value) => {
  activeFilter.value = value
}

const openProjectModal = (project) => {
  selectedProject.value = project
  showModal.value = true
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  showModal.value = false
  selectedProject.value = null
  document.body.style.overflow = 'auto'
}

// Computed
const filteredProjects = computed(() => {
  if (activeFilter.value === 'all') return projects.value
  return projects.value.filter(p =>
    p.categories.includes(activeFilter.value)
  )
})

const totalProjects = computed(() => projects.value.length)

const totalCommits = computed(() =>
  projects.value.reduce((sum, p) => sum + (p.stats?.commits || 0), 0)
)

const totalStars = computed(() =>
  projects.value.reduce((sum, p) => sum + (p.stats?.stars || 0), 0)
)
</script>