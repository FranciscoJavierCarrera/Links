<template>
  <div class="app">
    <!-- Profile Section -->
    <div class="profile-container">
      <div class="profile-image">
        <img 
          :src="profile.avatar" 
          :alt="profile.name"
          @error="handleImageError"
        />
      </div>
      
      <h1 class="profile-name">{{ profile.name }}</h1>
      <p class="profile-bio">{{ profile.bio }}</p>
    </div>

    <!-- Links Section -->
    <div class="links-container">
      <LinkButton
        v-for="link in links"
        :key="link.id"
        :title="link.title"
        :url="link.url"
        :icon="link.icon"
        @click="trackClick(link.title)"
      />
    </div>

    <!-- Social Links -->
    <div class="social-links">
      <SocialIcon
        v-for="social in socialLinks"
        :key="social.platform"
        :platform="social.platform"
        :url="social.url"
        :icon="social.icon"
      />
    </div>

    <!-- Footer -->
    <footer class="footer">
      <p>&copy; 2025 Mi LinkTree</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import LinkButton from './components/LinkButton.vue'
import SocialIcon from './components/SocialIcon.vue'

interface Link {
  id: number
  title: string
  url: string
  icon: string
}

interface SocialLink {
  platform: string
  url: string
  icon: string
}

interface Profile {
  name: string
  bio: string
  avatar: string
}

// Profile data
const profile = reactive<Profile>({
  name: 'María García',
  bio: '✨ Creadora de contenido | 🚀 Emprendedora | 💜 Amante del diseño',
  avatar: 'https://images.pexels.com/photos/774909/pexels-photo-774909.jpeg?auto=compress&cs=tinysrgb&w=300&h=300&dpr=1'
})

// Main links
const links = ref<Link[]>([
  {
    id: 1,
    title: 'Mi Blog Personal',
    url: 'https://blog.ejemplo.com',
    icon: 'blog'
  },
  {
    id: 2,
    title: 'Tienda Online',
    url: 'https://tienda.ejemplo.com',
    icon: 'shop'
  },
  {
    id: 3,
    title: 'Curso de Diseño',
    url: 'https://curso.ejemplo.com',
    icon: 'course'
  },
  {
    id: 4,
    title: 'Newsletter Gratuito',
    url: 'https://newsletter.ejemplo.com',
    icon: 'newsletter'
  },
  {
    id: 5,
    title: 'Consultoría 1:1',
    url: 'https://consultoria.ejemplo.com',
    icon: 'consulting'
  }
])

// Social links
const socialLinks = ref<SocialLink[]>([
  {
    platform: 'Instagram',
    url: 'https://instagram.com/usuario',
    icon: 'instagram'
  },
  {
    platform: 'Twitter',
    url: 'https://twitter.com/usuario',
    icon: 'twitter'
  },
  {
    platform: 'YouTube',
    url: 'https://youtube.com/usuario',
    icon: 'youtube'
  },
  {
    platform: 'LinkedIn',
    url: 'https://linkedin.com/in/usuario',
    icon: 'linkedin'
  }
])

// Methods
const handleImageError = (event: Event) => {
  const target = event.target as HTMLImageElement
  target.src = 'https://images.pexels.com/photos/1516680/pexels-photo-1516680.jpeg?auto=compress&cs=tinysrgb&w=300&h=300&dpr=1'
}

const trackClick = (linkTitle: string) => {
  console.log(`Clicked on: ${linkTitle}`)
  // Aquí podrías agregar analytics
}
</script>

<style scoped>
.app {
  min-height: 100vh;
  background: linear-gradient(135deg, #8B5CF6 0%, #3B82F6 100%);
  padding: 2rem 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}

.profile-container {
  text-align: center;
  margin-bottom: 2.5rem;
  animation: fadeInUp 0.8s ease-out;
}

.profile-image {
  margin-bottom: 1.5rem;
}

.profile-image img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.profile-image img:hover {
  transform: scale(1.05);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.profile-name {
  font-size: 2rem;
  font-weight: 700;
  color: white;
  margin: 0 0 0.5rem 0;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.profile-bio {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.9);
  margin: 0;
  max-width: 400px;
  line-height: 1.6;
}

.links-container {
  width: 100%;
  max-width: 480px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2.5rem;
}

.social-links {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
}

.footer {
  text-align: center;
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
}

.footer p {
  margin: 0;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .app {
    padding: 1.5rem 1rem;
  }
  
  .profile-name {
    font-size: 1.75rem;
  }
  
  .profile-bio {
    font-size: 1rem;
  }
  
  .links-container {
    max-width: 100%;
  }
}
</style>