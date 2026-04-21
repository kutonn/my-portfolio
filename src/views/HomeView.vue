<template>
  <div class="home">
    <!-- Hero -->
    <section class="hero">
      <div class="hero-content">
        <h1>{{ heroTitle }}</h1>
        <p class="hero-subtitle">{{ heroSubtitle }}</p>
        <div class="cta-buttons">
          <router-link to="/projects" class="btn btn-primary">
            <i class="fas fa-eye"></i> View Projects
          </router-link>
          <router-link to="/contact" class="btn btn-secondary">
            <i class="fas fa-paper-plane"></i> Contact
          </router-link>
        </div>
      </div>
    </section>

    <!-- About -->
    <section class="about">
      <div class="container">
        <h2 class="section-title">About Me</h2>
        <div class="about-grid">
          <div class="about-image">
            <!-- Replace icon with image -->
            <img 
              src="/src/assets/images/profile.gif" 
              alt="Your Name" 
              class="profile-img"
            >
          </div>
          <div class="about-text">
            <h3>{{ aboutTitle }}</h3>
            <p v-html="aboutDescription"></p>
            <div class="skills">
              <span v-for="skill in skills" :key="skill" class="skill-tag">
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const heroTitle = ref('Elton Jhon Pabuayon - Frontend Web Developer')
const heroSubtitle = ref('Crafting pixel-perfect digital experiences')
const aboutTitle = ref('Passionate Developer')
const aboutDescription = ref('5+ years of experience in layout designs, and a year of experience in building/configuring responsive web applications, whether for school purposes, or just a hobby.')
const skills = ref(['Vue.js', 'Node.js', 'Figma', 'TypeScript', 'Python', 'Android Studio', 'HTML', 'CSS', 'WordPress', 'Adobe Photoshop', 'Adobe InDesign', 'Adobe Illustrator', 'Canva'])
</script>

<style scoped>
/* Same modern CSS from previous version */
.home { min-height: 100vh; }
.hero { /* gradient background etc */ }
/* Copy full CSS from previous HTML version */
</style>