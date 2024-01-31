<script setup>
  import { ref } from 'vue'
  import TheHeader from './components/TheHeader.vue'
  import TheNav from './components/TheNav.vue'
  import TheTimeline from './pages/TheTimeline.vue'
  import TheActivities from './pages/TheActivities.vue'
  import TheProgress from './pages/TheProgress.vue'
  import { PAGE_ACTIVITIES, PAGE_PROGRESS, PAGE_TIMELINE } from './constants'

  const currPage = ref(normalizePageHash())

  function normalizePageHash() {
      const hash = window.location.hash.slice(1)

      if ([PAGE_ACTIVITIES, PAGE_PROGRESS, PAGE_TIMELINE].includes(hash) ) {
        return hash
      }
      
      window.location.hash = PAGE_TIMELINE

      return PAGE_TIMELINE
  }

</script>

<template>

  <TheHeader />

  <main class="flex flex-grow flex-col">
    <TheTimeline v-show="currPage === PAGE_TIMELINE" />
    <TheActivities v-show="currPage === PAGE_ACTIVITIES" />
    <TheProgress v-show="currPage === PAGE_PROGRESS" />
  </main>

  <TheNav :current-page="currPage" @navigate="currPage = $event" />
</template>
