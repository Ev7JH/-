<template>
  <div id="app">
    <div class="video-page">
      <div class="video-container">
        <video 
          ref="videoPlayer"
          autoplay
          loop
          playsinline
          muted
          class="video-player"
          :src="videoSource"
        >
          Ваш браузер не поддерживает видео.
        </video>
        
        <!-- Кнопка включения/выключения звука -->
        <button class="sound-button" @click="toggleSound">
          <svg v-if="!isMuted" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M3 9v6h4l5 5V4L7 9H3zm13.5 3c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02zM14 3.23v2.06c2.89.86 5 3.54 5 6.71s-2.11 5.85-5 6.71v2.06c4.01-.91 7-4.49 7-8.77s-2.99-7.86-7-8.77z"/>
          </svg>
          <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M16.5 12c0-1.77-1.02-3.29-2.5-4.03v2.21l2.45 2.45c.03-.2.05-.41.05-.63zm2.5 0c0 .94-.2 1.82-.54 2.64l1.51 1.51c.66-1.24 1.03-2.61 1.03-4.15 0-4.28-2.99-7.86-7-8.77v2.06c2.89.86 5 3.54 5 6.71zM4.27 3L3 4.27 7.73 9H3v6h4l5 5v-6.73l4.25 4.25c-.67.52-1.42.93-2.25 1.18v2.06c1.38-.31 2.63-.95 3.69-1.81L19.73 21 21 19.73l-9-9L4.27 3zM12 4L9.91 6.09 12 8.18V4z"/>
          </svg>
        </button>
      </div>

      <div class="social-links">
        <a 
          :href="instagramLink" 
          target="_blank" 
          rel="noopener noreferrer"
          class="social-link instagram"
        >
          <svg class="social-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M12 2c2.717 0 3.056.01 4.122.06 1.065.05 1.79.217 2.428.465.66.254 1.216.598 1.772 1.153.509.5.902 1.105 1.153 1.772.247.637.415 1.363.465 2.428.047 1.066.06 1.405.06 4.122 0 2.717-.01 3.056-.06 4.122-.05 1.065-.218 1.79-.465 2.428-.254.66-.598 1.216-1.153 1.772-.5.509-1.105.902-1.772 1.153-.637.247-1.363.415-2.428.465-1.066.047-1.405.06-4.122.06-2.717 0-3.056-.01-4.122-.06-1.065-.05-1.79-.218-2.428-.465-.66-.254-1.216-.598-1.772-1.153-.509-.5-.902-1.105-1.153-1.772-.247-.637-.415-1.363-.465-2.428-.047-1.066-.06-1.405-.06-4.122 0-2.717.01-3.056.06-4.122.05-1.065.218-1.79.465-2.428.254-.66.598-1.216 1.153-1.772.5-.509 1.105-.902 1.772-1.153.637-.247 1.363-.415 2.428-.465C8.944 2.01 9.283 2 12 2zm0 5a5 5 0 100 10 5 5 0 000-10zm6.5-.25a1.25 1.25 0 10-2.5 0 1.25 1.25 0 002.5 0zM12 9a3 3 0 110 6 3 3 0 010-6z"/>
          </svg>
          <span>Instagram</span>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      videoSource: '/videos/my-video.mp4',
      instagramLink: 'https://www.instagram.com/kasschey?igsh=cjRuanlkMHJwOHF4',
      isMuted: true
    }
  },
  mounted() {
    const video = this.$refs.videoPlayer
    if (video) {
      video.play().catch(error => {
        console.log('Автозапуск:', error)
      })
      
      video.addEventListener('contextmenu', (e) => {
        e.preventDefault()
      })
    }
  },
  methods: {
    toggleSound() {
      const video = this.$refs.videoPlayer
      if (video) {
        video.muted = !video.muted
        this.isMuted = video.muted
        if (!video.muted) {
          video.volume = 0.6
        }
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  min-height: 100vh;
  width: 100%;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

/* Минималистический тёмный фон */
.video-page {
  width: 100%;
  min-height: 100vh;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #0a0a0a;
  background-image: radial-gradient(circle at 25% 40%, rgba(30, 30, 40, 0.5) 0%, #0a0a0a 100%);
}

.video-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  margin-bottom: 40px;
  background: #000;
}

.video-player {
  width: 100%;
  display: block;
  object-fit: cover;
}

/* Кнопка звука - минималистичная */
.sound-button {
  position: absolute;
  bottom: 16px;
  right: 16px;
  background: rgba(20, 20, 25, 0.8);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 40px;
  width: 40px;
  height: 40px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  color: rgba(255, 255, 255, 0.8);
}

.sound-button:hover {
  background: rgba(40, 40, 48, 0.9);
  color: white;
  transform: scale(1.05);
}

.sound-button svg {
  width: 20px;
  height: 20px;
}

/* Социальная кнопка - только Instagram */
.social-links {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
  width: 100%;
  max-width: 800px;
}

.social-link {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 10px 28px;
  border-radius: 40px;
  text-decoration: none;
  font-weight: 500;
  font-size: 15px;
  transition: all 0.2s ease;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: rgba(255, 255, 255, 0.85);
  letter-spacing: 0.3px;
}

.social-link:hover {
  background: rgba(255, 255, 255, 0.12);
  border-color: rgba(255, 255, 255, 0.15);
  transform: translateY(-2px);
  color: white;
}

.social-icon {
  width: 20px;
  height: 20px;
}

/* Адаптация для планшетов */
@media (max-width: 768px) {
  .video-page {
    padding: 16px;
  }
  
  .video-container {
    max-width: 95%;
    border-radius: 20px;
  }
  
  .social-link {
    padding: 8px 24px;
    font-size: 14px;
    gap: 8px;
  }
  
  .social-icon {
    width: 18px;
    height: 18px;
  }
  
  .sound-button {
    width: 36px;
    height: 36px;
    bottom: 12px;
    right: 12px;
  }
}

/* Адаптация для телефонов */
@media (max-width: 480px) {
  .video-page {
    padding: 12px;
  }
  
  .video-container {
    max-width: 100%;
    border-radius: 18px;
    margin-bottom: 24px;
  }
  
  .social-link {
    padding: 7px 20px;
    font-size: 13px;
    gap: 7px;
  }
  
  .social-icon {
    width: 16px;
    height: 16px;
  }
  
  .sound-button {
    width: 32px;
    height: 32px;
    bottom: 10px;
    right: 10px;
  }
  
  .sound-button svg {
    width: 16px;
    height: 16px;
  }
}

/* Для больших экранов */
@media (min-width: 1200px) {
  .video-container {
    max-width: 900px;
  }
  
  .social-links {
    max-width: 900px;
  }
  
  .social-link {
    padding: 12px 32px;
    font-size: 16px;
  }
  
  .sound-button {
    width: 44px;
    height: 44px;
  }
}

/* Убираем эффекты нажатия на сенсорных устройствах */
@media (hover: none) and (pointer: coarse) {
  .social-link:hover {
    transform: none;
  }
  
  .social-link:active {
    transform: scale(0.96);
  }
}
</style>