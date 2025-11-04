<template>
  <div class="home-ad-banner" v-if="showAds">
    <div class="ad-wrapper">
      <ins class="adsbygoogle"
           style="display:block"
           data-ad-client="ca-pub-8275085702635989"
           data-ad-format="auto"
           data-full-width-responsive="true"></ins>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const showAds = ref(false)

onMounted(() => {
  if (typeof window !== 'undefined') {
    try {
      (window.adsbygoogle = window.adsbygoogle || []).push({})
      showAds.value = true
    } catch (e) {
      console.log('AdSense error:', e)
    }
  }
})
</script>

<style scoped>
.home-ad-banner {
  width: 100%;
  max-width: 1200px;
  margin: 3rem auto;
  padding: 0 2rem;
}

.ad-wrapper {
  background: rgba(255, 255, 255, 0.03);
  border-radius: 12px;
  padding: 1.5rem;
  min-height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px dashed rgba(255, 255, 255, 0.1);
}

@media (max-width: 768px) {
  .home-ad-banner {
    margin: 2rem auto;
    padding: 0 1rem;
  }
  
  .ad-wrapper {
    padding: 1rem;
    min-height: 80px;
  }
}
</style>

