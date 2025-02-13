<script setup>
import {reactive, onMounted, ref} from 'vue';
import JobLisiting from './JobLisiting.vue';
import {RouterLink} from 'vue-router'
import axios from 'axios';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';


const state = reactive({
    isLoading: true,
    jobs: []
});

const props = defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }
});

onMounted(async()=>{
    try {
        const { data } = await axios.get('http://localhost:5000/jobs');
        state.jobs = data;
    } catch (error) {
        console.log("Error Fetching Jobs:", error)
    } finally{
        state.isLoading = false;
    }
});

</script>

<template>
    <section class="job-section">
      <div class="container">
        <h2 class="section-title">Browse Jobs</h2>
  
        <!-- Show loading spinner while loading is true -->
        <div v-if="state.isLoading" class="loading">
          <PulseLoader />
        </div>
        <!-- Show job listing when done loading -->
        <div v-else class="job-grid">
          <JobLisiting
            v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
            :key="job.id"
            :job="job"
          />
        </div>
      </div>
    </section>
  
    <section v-if="showButton" class="button-section">
      <RouterLink to="/jobs" class="view-jobs-button">
        View All Jobs
      </RouterLink>
    </section>

  </template>
  
  <style scoped>
  /* Job Section */
  .job-section {
    background-color: #eff6ff; /* Equivalent to bg-blue-50 */
    padding: 40px 16px;
  }
  
  /* Container */
  .container {
    max-width: 1200px;
    margin: auto;
    text-align: center;
  }
  
  /* Title */
  .section-title {
    font-size: 24px;
    font-weight: bold;
    color: #22c55e; /* Equivalent to text-green-500 */
    margin-bottom: 24px;
  }
  
  /* Loading Spinner */
  .loading {
    color: #6b7280; /* Equivalent to text-gray-500 */
    padding: 24px 0;
  }
  
  /* Job Grid */
  .job-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 24px;
  }
  
  /* Responsive for Medium Screens (md:grid-cols-3) */
  @media (min-width: 768px) {
    .job-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }
  
  /* View Jobs Button Section */
  .button-section {
    max-width: 600px;
    margin: 40px auto;
    padding: 0 24px;
  }
  
  /* View Jobs Button */
  .view-jobs-button {
    display: block;
    background-color: black;
    color: white;
    text-align: center;
    padding: 16px 24px;
    border-radius: 12px;
    text-decoration: none;
    font-weight: bold;
    transition: background-color 0.3s ease;
  }
  
  .view-jobs-button:hover {
    background-color: #374151; /* Equivalent to hover:bg-gray-700 */
  }
  </style>
  