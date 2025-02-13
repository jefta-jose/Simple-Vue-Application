<script setup>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import {reactive, onMounted} from 'vue';
import { useRoute, RouterLink, useRouter } from 'vue-router';
import axios from 'axios';
import BackButton from '@/components/BackButton.vue';
import { useToast } from 'vue-toastification';

const route = useRoute();
const router = useRouter();
const toast = useToast();

const jobId = route.params.id;

console.log("jobId:", jobId);

const state = reactive({
    job:{},
    isLoading: true,
});

const deleteJob = async()=>{
  try {
    await axios.delete(`http://localhost:5000/jobs/${jobId}`);
    toast.success("Job Deleted Successfully")
    router.push('/jobs')
  } catch (error) {
    console.log("Error Deleting Job:", error);
    toast.error("Error Deleting Job");
  }
}

onMounted(async () => {
    try {
        const {data} = await axios.get(`http://localhost:5000/jobs/${jobId}`);
        state.job = data;
    } catch (error) {
        console.log('Error Fetching Job:', error);
    } finally{
        state.isLoading = false;
    }
});

</script>

<template>
    <BackButton />
    <section v-if="!state.isLoading" class="job-section">
      <div class="container">
        <div class="job-layout">
          <main>
            <div class="job-card">
              <div class="job-type">{{ state.job.type }}</div>
              <h1 class="job-title">{{ state.job.title }}</h1>
              <div class="job-location">
                <i class="pi pi-map-marker location-icon"></i>
                <p>{{ state.job.location }}</p>
              </div>
            </div>
  
            <div class="job-details">
              <h3>Job Description</h3>
              <p>{{ state.job.description }}</p>
  
              <h3>Salary</h3>
              <p>{{ state.job.salary }} / Year</p>
            </div>
          </main>
  
          <!-- Sidebar -->
          <aside>
            <!-- Company Info -->
            <div class="company-info">
              <h3>Company Info</h3>
              <h2>{{ state.job.company.name }}</h2>
              <p>{{ state.job.company.description }}</p>
              <hr />
              <h3>Contact Email:</h3>
              <p class="contact-info">{{ state.job.company.contactEmail }}</p>
              <h3>Contact Phone:</h3>
              <p class="contact-info">{{ state.job.company.contactPhone }}</p>
            </div>
  
            <!-- Manage -->
            <div class="manage-job">
              <h3>Manage Job</h3>
              <RouterLink :to="`/jobs/edit/${state.job.id}`" class="edit-button">Edit Job</RouterLink>
              <button @click="deleteJob" class="delete-button">Delete Job</button>
            </div>
          </aside>
        </div>
      </div>
    </section>
  
    <div v-else class="loading-state">
      <PulseLoader />
    </div>
  </template>

<style scoped>
/* Container */
.container {
  width: 90%;
  max-width: 1200px;
  margin: auto;
  padding: 40px 20px;
}

/* Layout */
.job-layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}

@media (min-width: 768px) {
  .job-layout {
    grid-template-columns: 70% 30%;
  }
}

/* Job Card */
.job-card {
  background: white;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
}

@media (min-width: 768px) {
  .job-card {
    text-align: left;
  }
}

.job-type {
  color: gray;
  margin-bottom: 16px;
}

.job-title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 16px;
}

.job-location {
  color: #d97706;
  display: flex;
  align-items: center;
  justify-content: center;
}

@media (min-width: 768px) {
  .job-location {
    justify-content: flex-start;
  }
}

.location-icon {
  font-size: 18px;
  margin-right: 8px;
}

/* Job Details */
.job-details {
  background: white;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  margin-top: 24px;
}

.job-details h3 {
  color: #065f46;
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 12px;
}

/* Sidebar */
.company-info,
.manage-job {
  background: white;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  margin-top: 24px;
}

.company-info h3,
.manage-job h3 {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 12px;
}

.contact-info {
  background: #d1fae5;
  padding: 8px;
  font-weight: bold;
  margin: 8px 0;
}

/* Buttons */
.edit-button,
.delete-button {
  display: block;
  width: 100%;
  text-align: center;
  padding: 12px;
  border-radius: 24px;
  font-weight: bold;
  cursor: pointer;
  text-decoration: none;
}

.edit-button {
  background: #10b981;
  color: white;
  margin-top: 16px;
}

.edit-button:hover {
  background: #059669;
}

.delete-button {
  background: #ef4444;
  color: white;
  margin-top: 16px;
}

.delete-button:hover {
  background: #dc2626;
}

/* Loading State */
.loading-state {
  text-align: center;
  color: gray;
  padding: 24px;
}

</style>