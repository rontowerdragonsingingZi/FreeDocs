<template>
  <div class="ad-redirect-page">
    <div class="ad-content">
      <div class="ad-header">
        <h1>{{ title }}</h1>
        <p class="subtitle">{{ subtitle }}</p>
      </div>
      
      <!-- Google AdSense 广告位 - 主要广告 -->
      <div class="ad-container main-ad" v-if="showAds">
        <ins class="adsbygoogle"
             style="display:block"
             data-ad-client="ca-pub-8275085702635989"
             data-ad-format="auto"
             data-full-width-responsive="true"></ins>
      </div>
      
      <!-- 倒计时和继续按钮 -->
      <div class="action-section">
        <div class="countdown" v-if="countdown > 0">
          <p>{{ countdownText }}: <span class="countdown-number">{{ countdown }}</span></p>
        </div>
        <button 
          class="continue-button" 
          :disabled="countdown > 0"
          @click="handleContinue"
        >
          {{ buttonText }}
        </button>
      </div>
      
      <!-- Google AdSense 广告位 - 底部广告 -->
      <div class="ad-container bottom-ad" v-if="showAds">
        <ins class="adsbygoogle"
             style="display:block"
             data-ad-client="ca-pub-8275085702635989"
             data-ad-format="auto"
             data-full-width-responsive="true"></ins>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  title: {
    type: String,
    default: '正在为您准备 API Key'
  },
  subtitle: {
    type: String,
    default: '感谢您的耐心等待，我们正在处理您的请求'
  },
  countdownText: {
    type: String,
    default: '请等待'
  },
  buttonText: {
    type: String,
    default: '继续获取 API Key'
  },
  redirectUrl: {
    type: String,
    default: '/contact'
  },
  countdownSeconds: {
    type: Number,
    default: 5
  }
})

const countdown = ref(props.countdownSeconds)
const showAds = ref(false)
let countdownTimer = null

const handleContinue = () => {
  // 跳转到实际获取API Key的页面（联系页面或表单页面）
  window.location.href = props.redirectUrl
}

onMounted(() => {
  // 启动倒计时
  countdownTimer = setInterval(() => {
    if (countdown.value > 0) {
      countdown.value--
    } else {
      clearInterval(countdownTimer)
    }
  }, 1000)
  
  // 加载谷歌广告脚本
  if (typeof window !== 'undefined') {
    // 加载 Google AdSense 脚本
    const script = document.createElement('script')
    script.async = true
    script.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-8275085702635989'
    script.crossOrigin = 'anonymous'
    document.head.appendChild(script)
    
    script.onload = () => {
      try {
        (window.adsbygoogle = window.adsbygoogle || []).push({})
        showAds.value = true
      } catch (e) {
        console.log('AdSense error:', e)
      }
    }
  }
})

onUnmounted(() => {
  if (countdownTimer) {
    clearInterval(countdownTimer)
  }
})
</script>

<style scoped>
.ad-redirect-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  min-height: 70vh;
}

.ad-content {
  background: linear-gradient(135deg, rgba(91, 44, 191, 0.05) 0%, rgba(0, 217, 255, 0.05) 100%);
  border-radius: 20px;
  padding: 3rem;
  backdrop-filter: blur(10px);
}

.ad-header {
  text-align: center;
  margin-bottom: 2rem;
}

.ad-header h1 {
  font-size: 2rem;
  font-weight: 700;
  background: linear-gradient(135deg, #5b2cbf 0%, #00d9ff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 1rem;
}

.subtitle {
  font-size: 1.1rem;
  color: var(--vp-c-text-2);
}

.ad-container {
  margin: 2rem 0;
  padding: 1.5rem;
  background: rgba(255, 255, 255, 0.03);
  border-radius: 12px;
  min-height: 250px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px dashed rgba(255, 255, 255, 0.1);
}

.main-ad {
  min-height: 300px;
}

.bottom-ad {
  min-height: 200px;
}

.action-section {
  text-align: center;
  margin: 2rem 0;
  padding: 2rem;
}

.countdown {
  margin-bottom: 1.5rem;
}

.countdown p {
  font-size: 1.2rem;
  color: var(--vp-c-text-1);
}

.countdown-number {
  font-size: 2rem;
  font-weight: 700;
  background: linear-gradient(135deg, #5b2cbf 0%, #00d9ff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: inline-block;
  min-width: 40px;
}

.continue-button {
  padding: 1rem 3rem;
  font-size: 1.1rem;
  font-weight: 600;
  color: white;
  background: linear-gradient(135deg, #5b2cbf 0%, #00d9ff 100%);
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(91, 44, 191, 0.3);
}

.continue-button:not(:disabled):hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(91, 44, 191, 0.4);
}

.continue-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  filter: grayscale(50%);
}

@media (max-width: 768px) {
  .ad-content {
    padding: 1.5rem;
  }
  
  .ad-header h1 {
    font-size: 1.5rem;
  }
  
  .ad-container {
    padding: 1rem;
    min-height: 200px;
  }
  
  .main-ad {
    min-height: 250px;
  }
}
</style>

