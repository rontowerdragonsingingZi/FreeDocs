<template>
  <div class="home-ad-banner">
    <div class="free-text">{{ freeText }}</div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useData } from 'vitepress'

const { page } = useData()

const freeText = computed(() => {
  // 根據當前路徑判斷語言
  const path = page.value.relativePath || ''
  return path.startsWith('en/') ? 'FREE!' : '免費！'
})
</script>

<style scoped>
.home-ad-banner {
  width: 100%;
  position: relative;
  min-height: 200px;
  display: flex;
  justify-content: flex-start;
  align-items: flex-end;
  padding-left: 5%;
  padding-bottom: 2rem;
}

.free-text {
  font-size: 10rem;
  font-weight: 900;
  font-family: 'Arial Black', 'Microsoft YaHei', sans-serif;
  color: transparent;
  -webkit-text-stroke: 3px rgba(128, 128, 128, 0.15);
  text-stroke: 3px rgba(128, 128, 128, 0.15);
  transform: rotate(-8deg);
  letter-spacing: 0.05em;
  user-select: none;
  pointer-events: none;
}

@media (max-width: 768px) {
  .home-ad-banner {
    padding-left: 3%;
  }

  .free-text {
    font-size: 6rem;
  }
}

@media (max-width: 480px) {
  .free-text {
    font-size: 4rem;
  }
}
</style>

