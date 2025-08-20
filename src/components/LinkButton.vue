<template>
  <a 
    :href="url" 
    target="_blank" 
    rel="noopener noreferrer"
    class="link-button"
    @click="$emit('click')"
  >
    <div class="icon-container">
      <component :is="iconComponent" class="icon" />
    </div>
    <span class="title">{{ title }}</span>
    <div class="arrow">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
        <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>
  </a>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import BlogIcon from './icons/BlogIcon.vue'
import ShopIcon from './icons/ShopIcon.vue'
import CourseIcon from './icons/CourseIcon.vue'
import NewsletterIcon from './icons/NewsletterIcon.vue'
import ConsultingIcon from './icons/ConsultingIcon.vue'

interface Props {
  title: string
  url: string
  icon: string
}

defineEmits<{
  click: []
}>()

const iconComponents = {
  blog: BlogIcon,
  shop: ShopIcon,
  course: CourseIcon,
  newsletter: NewsletterIcon,
  consulting: ConsultingIcon
}

const iconComponent = computed(() => {
  return iconComponents[props.icon as keyof typeof iconComponents] || BlogIcon
})

const props = defineProps<Props>()
</script>

<style scoped>
.link-button {
  display: flex;
  align-items: center;
  padding: 1rem 1.5rem;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  text-decoration: none;
  color: #374151;
  font-weight: 600;
  font-size: 1rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  border: 2px solid transparent;
  position: relative;
  overflow: hidden;
}

.link-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.6s ease;
}

.link-button:hover::before {
  left: 100%;
}

.link-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
  border-color: rgba(139, 92, 246, 0.3);
  background: rgba(255, 255, 255, 1);
}

.link-button:active {
  transform: translateY(0);
}

.icon-container {
  flex-shrink: 0;
  margin-right: 1rem;
}

.icon {
  width: 24px;
  height: 24px;
  color: #8B5CF6;
}

.title {
  flex-grow: 1;
  text-align: left;
}

.arrow {
  flex-shrink: 0;
  color: #9CA3AF;
  transition: transform 0.3s ease;
}

.link-button:hover .arrow {
  transform: translateX(4px);
  color: #8B5CF6;
}

@media (max-width: 768px) {
  .link-button {
    padding: 1rem;
    font-size: 0.95rem;
  }
  
  .icon-container {
    margin-right: 0.75rem;
  }
}
</style>