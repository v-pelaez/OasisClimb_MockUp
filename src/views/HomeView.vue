<script setup lang="ts">
import HeaderComponent from '../components/HeaderComponent.vue'
import FooterComponent from '../components/FooterComponent.vue'
import RankingComponent from '../components/RankingComponent.vue'
import NewsComponent from '../components/NewsComponent.vue'
import MarkFormComponent from '@/components/MarkFormComponent.vue'
import BackgroundComponent from '@/components/BackgroundComponent.vue'
import ScrollTopComponent from '@/components/ScrollTopComponent.vue'
import AboutUsComponent from '@/components/AboutUsComponent.vue'
import VideoCarouselComponent from '@/components/VideoCarouselComponent.vue'

</script>

<template>
  <main>
    <HeaderComponent />
    <VideoCarouselComponent/>
    <ScrollTopComponent />
    <BackgroundComponent />
    <NewsComponent />
    <RankingComponent />
    <MarkFormComponent />
    <AboutUsComponent />
    <FooterComponent />
  </main>
</template>
