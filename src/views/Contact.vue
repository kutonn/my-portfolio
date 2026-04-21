<template>
  <section class="contact">
    <div class="section-header">
      <h2 class="section-title">Get In Touch</h2>
      <p class="section-subtitle">
      Feel free to reach out for collaborations or opportunities
      </p>
      <div class="contact-grid">
        <!-- LEFT: Profile + Contact Info -->
        <div class="contact-left">
          <div class="profile-section">
            <h3 class="profile-name">{{ profileName }}</h3>
            <p class="profile-role">{{ profileRole }}</p>
          </div>
          
          <!-- Contact Details -->
          <div class="contact-info">
            <h4>Let's Connect</h4>
            <div class="contact-item" v-for="item in contactItems" :key="item.icon">
              <i :class="item.icon"></i>
              <div>
                <strong>{{ item.label }}</strong>
                <div>{{ item.value }}</div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- RIGHT: Contact Form -->
        <div class="contact-form-container">
          <form class="contact-form">
            <div class="form-group">
              <label>Name</label>
              <input type="text" v-model="form.name" required>
            </div>
            <div class="form-group">
              <label>Email</label>
              <input type="email" v-model="form.email" required>
            </div>
            <div class="form-group">
              <label>Message</label>
              <textarea v-model="form.message" required></textarea>
            </div>
            <button type="submit" class="btn btn-primary btn-full">
              Send Message
              <i class="fas fa-paper-plane ml-2"></i>
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Profile Data
const profileName = ref('Elton Jhon Pabuayon')
const profileRole = ref('Front-End Web Developer & Designer')

// Contact Info
const contactItems = ref([
  { icon: 'fas fa-envelope', label: 'Email', value: 'eltonjhonmartinez@outlook.com' },
  { icon: 'fas fa-map-marker-alt', label: 'Location', value: 'Manila City, Philippines' },
  { icon: 'fas fa-phone', label: 'Phone', value: '+63 976 1793 563' },
  { icon: 'fas fa-globe', label: 'Github', value: 'github.com/kutonn' }
])

// Form Data
const form = ref({
  name: '',
  email: '',
  message: ''
})
</script>