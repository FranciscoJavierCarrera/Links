<template>
  <a 
    :href="url" 
    target="_blank" 
    rel="noopener noreferrer"
    class="social-icon"
    :aria-label="platform"
  >
    <component :is="iconComponent" class="icon" />
  </a>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import InstagramIcon from './icons/InstagramIcon.vue'
import TwitterIcon from './icons/TwitterIcon.vue'
import YouTubeIcon from './icons/YouTubeIcon.vue'
import LinkedInIcon from './icons/LinkedInIcon.vue'

interface Props {
  platform: string
  url: string
  icon: string
}

const props = defineProps<Props>()

const iconComponents = {
  instagram: InstagramIcon,
  twitter: TwitterIcon,
  youtube: YouTubeIcon,
  linkedin: LinkedInIcon
}

const iconComponent = computed(() => {
  return iconComponents[props.icon as keyof typeof iconComponents] || InstagramIcon
})
</script>

<style scoped>
.social-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  border-radius: 12px;
  text-decoration: none;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.social-icon:hover {
  background: rgba(255, 255, 255, 0.95);
  transform: translateY(-2px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  border-color: rgba(255, 255, 255, 0.3);
}

.icon {
  width: 24px;
  height: 24px;
  color: white;
  transition: color 0.3s ease;
}

.social-icon:hover .icon {
  color: #8B5CF6;
}

@media (max-width: 768px) {
  .social-icon {
    width: 44px;
    height: 44px;
  }
  
  .icon {
    width: 22px;
    height: 22px;
  }
}
</style>