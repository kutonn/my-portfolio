<template>
  <nav class="navbar">
    <div class="nav-container">
      <!-- Logo LEFT -->
      <router-link to="/" class="logo">Elton Jhon Pabuayon</router-link>
      
      <!-- CENTER NAV LINKS -->
      <div class="nav-center">
        <router-link to="/" class="nav-link">Home</router-link>
        <router-link to="/projects" class="nav-link">Projects</router-link>
        <router-link to="/contact" class="nav-link">Contact</router-link>
      </div>
      
      <!-- CTA BUTTON RIGHT (Optional) -->
      <a href="mailto:eltonjhonmartinez@outlook.com" class="btn btn-sm">Hire Me</a>
    </div>
  </nav>
</template>