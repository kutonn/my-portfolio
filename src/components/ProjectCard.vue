 <template>
  <div class="project-card" @click="$emit('click')">
    <div class="project-image">
      <div class="image-placeholder">
        <img
        v-for="(img, index) in project.screenshots?.length ? project.screenshots : [project.image]"
        :key="index"
        :src="img"
        class="preview-image"
        :class="{ active: currentIndex === index }"/>
        <div class="overlay">
          <h3>Click to Preview</h3>
        </div>
      </div>
    </div>
    <div class="project-content">
      <h2>{{ project.title }}</h2>
      <p>{{ project.description }}</p>
      <div class="tech-list">
        <span v-for="tech in project.tech" :key="tech">{{ tech }}</span>
      </div>
      <div class="project-actions">
        <a 
        :href="project.liveDemo" 
        target="_blank" 
        class="btn-live"
        @click.stop
        >
        {{ project.liveLabel || 'Live Demo' }}
      </a>
        <a 
        :href="project.github" 
        target="_blank" 
        class="btn-code"
        @click.stop
        >
        {{ project.codeLabel || 'View Code' }}
      </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  project: Object
})

const currentIndex = ref(0)
let interval = null

onMounted(() => {
  const images = props.project?.screenshots?.length
    ? props.project.screenshots
    : [props.project.image]

  if (!images.length) return

  interval = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % images.length
  }, 2000)
})

onUnmounted(() => {
  clearInterval(interval)
})

</script>

<style scoped>
.project-card {
  background: white;
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.1);
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
  height: 100%;
}

.project-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 60px rgba(0,0,0,0.2);
}

.project-image {
  height: 250px;
  overflow: hidden;
}

.image-placeholder {
  height: 100%;
  background: linear-gradient(135deg, #667eea, #764ba2);
  background-size: cover;
  background-position: center;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.overlay {
  background: rgba(0,0,0,0.8);
  color: white;
  padding: 2rem;
  text-align: center;
  border-radius: 0 0 20px 20px;
  width: 100%;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.project-card:hover .overlay {
  transform: translateY(0);
}

.project-content {
  padding: 2rem;
}

.project-content h2 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #1f2937;
}

.project-content p {
  color: #64748b;
  margin-bottom: 1.5rem;
}

.tech-list {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.tech-list span {
  background: #eff6ff;
  color: #2563eb;
  padding: 0.25rem 0.75rem;
  border-radius: 15px;
  font-size: 0.8rem;
  font-weight: 500;
}

.project-actions {
  display: flex;
  gap: 1rem;
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

.btn-live:hover, .btn-code:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

.preview-image {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  top: 0;
  left: 0;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.preview-image.active {
  opacity: 1;
  z-index: 1;
}
</style>