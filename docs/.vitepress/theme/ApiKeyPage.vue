<template>
  <div class="api-key-page">
    <div class="api-key-container">
      <div class="api-key-header">
        <h1>{{ title }}</h1>
        <p class="subtitle">{{ subtitle }}</p>
      </div>
      
      <div class="api-key-methods">
        <div class="method-card">
          <div class="method-icon">📱</div>
          <h3>{{ phoneTitle }}</h3>
          <p>{{ phoneDesc }}</p>
          <button class="method-button" @click="handlePhoneMethod">
            {{ phoneButtonText }}
          </button>
        </div>
        
        <div class="method-card">
          <div class="method-icon">🌐</div>
          <h3>{{ onlineTitle }}</h3>
          <p>{{ onlineDesc }}</p>
          <button class="method-button primary" @click="handleOnlineMethod">
            {{ onlineButtonText }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  title: {
    type: String,
    default: '获取 API Key'
  },
  subtitle: {
    type: String,
    default: '选择您喜欢的方式获取 API Key'
  },
  phoneTitle: {
    type: String,
    default: '手机获取'
  },
  phoneDesc: {
    type: String,
    default: '通过手机扫描二维码或访问链接获取 API Key'
  },
  phoneButtonText: {
    type: String,
    default: '使用手机获取'
  },
  onlineTitle: {
    type: String,
    default: '在线获取'
  },
  onlineDesc: {
    type: String,
    default: '在线填写表单即可快速获取 API Key'
  },
  onlineButtonText: {
    type: String,
    default: '在线获取 API Key'
  },
  adPageUrl: {
    type: String,
    default: '/ad-redirect'
  }
})

const handlePhoneMethod = () => {
  alert('手机获取功能开发中，请使用在线获取方式')
}

const handleOnlineMethod = () => {
  window.location.href = props.adPageUrl
}
</script>

<style scoped>
.api-key-page {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.api-key-container {
  background: var(--vp-c-bg-soft);
  border: 1px solid var(--vp-c-divider);
  border-radius: 8px;
  padding: 3rem 2rem;
}

.api-key-header {
  text-align: center;
  margin-bottom: 3rem;
}

.api-key-header h1 {
  font-size: 2rem;
  font-weight: 600;
  color: var(--vp-c-text-1);
  margin-bottom: 0.5rem;
}

.subtitle {
  font-size: 1rem;
  color: var(--vp-c-text-2);
}

.api-key-methods {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.method-card {
  background: var(--vp-c-bg);
  border: 1px solid var(--vp-c-divider);
  border-radius: 8px;
  padding: 2rem 1.5rem;
  text-align: center;
  transition: all 0.2s ease;
}

.method-card:hover {
  border-color: var(--vp-c-brand-1);
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
}

.method-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.method-card h3 {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.75rem;
  color: var(--vp-c-text-1);
}

.method-card p {
  font-size: 0.9rem;
  color: var(--vp-c-text-2);
  margin-bottom: 1.5rem;
  line-height: 1.5;
}

.method-button {
  padding: 0.625rem 1.5rem;
  border-radius: 6px;
  border: 1px solid var(--vp-c-divider);
  background: var(--vp-c-bg);
  font-size: 0.95rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
  color: var(--vp-c-text-1);
}

.method-button:hover {
  border-color: var(--vp-c-brand-1);
  color: var(--vp-c-brand-1);
}

.method-button.primary {
  background: var(--vp-c-brand-1);
  border-color: var(--vp-c-brand-1);
  color: #fff;
}

.method-button.primary:hover {
  background: var(--vp-c-brand-2);
  border-color: var(--vp-c-brand-2);
}

@media (max-width: 768px) {
  .api-key-container {
    padding: 2rem 1.5rem;
  }
  
  .api-key-header h1 {
    font-size: 1.75rem;
  }
  
  .api-key-methods {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
}
</style>

