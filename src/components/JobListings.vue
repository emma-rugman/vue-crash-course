<script setup lang="ts">
  import JobListing from '@/components/JobListing.vue';
  import { ref, defineProps, onMounted, reactive } from 'vue'
  import { RouterLink } from 'vue-router';
  import axios from 'axios';

  const jobs = ref([]);

  // can also use reactive as opposed to ref - only for objects
  // and cannot be reassigned e.g. see below. Don't use .value
  // instead would use e.g. state.jobs and state.isLoading to
  // reference
  // const state = reactive({
  //   jobs: [],
  //   isLoading: true,
  // })

  defineProps({
    limit: Number,
    showButton: {
      type: Boolean,
      default: false
    }
  })

  onMounted(async () => {
    try {
      const response = await axios.get('http://localhost:5000/jobs');
      jobs.value = response.data;
    } catch (error) {
      console.error(`Error fetching jobs: ${ error }`);
    }
  });
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
      </div>
    </div>
  </section>

  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
    >View All Jobs</RouterLink
    >
  </section>

</template>
