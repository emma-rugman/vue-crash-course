<script setup lang="ts">
import HeroMain from '@/components/HeroMain.vue';
import HomeCards from '@/components/HomeCards.vue';
import JobListings from '@/components/JobListings.vue';
</script>

<template>
  <HeroMain title = 'Test Title' subtitle = 'Test subtitle'/>
  <HomeCards />
  <JobListings :limit="3" :showButton="true"/>
</template>
