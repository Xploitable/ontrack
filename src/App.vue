<script setup>
  import { ref } from 'vue'
  import TheHeader from './components/TheHeader.vue'
  import TheNav from './components/TheNav.vue'
  import TheTimeline from './pages/TheTimeline.vue'
  import TheActivities from './pages/TheActivities.vue'
  import TheProgress from './pages/TheProgress.vue'
  import { PAGE_ACTIVITIES, PAGE_PROGRESS, PAGE_TIMELINE } from './constants'
  import { normalizePageHash, generateTimelineItems } from './functions'

  const currentPage = ref(normalizePageHash())

  function goTo(page) {
    currentPage.value = page
  }

  const timelineItems = generateTimelineItems()
</script>

<template>

  <TheHeader 
    @go-to-timeline="goTo(PAGE_TIMELINE)" 
    @go-to-progress="goTo(PAGE_PROGRESS)"
  />

  <main class="flex flex-grow flex-col">
    <TheTimeline v-show="currentPage === PAGE_TIMELINE" :timeline-items="timelineItems"/>
    <TheActivities v-show="currentPage === PAGE_ACTIVITIES" />
    <TheProgress v-show="currentPage === PAGE_PROGRESS" />
  </main>

  <TheNav :current-page="currentPage" @navigate="currentPage = $event" />
</template>
