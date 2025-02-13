<script setup>
import {RouterLink} from 'vue-router'
import {ref, computed} from 'vue';

const props = defineProps({
    job: Object
});

console.log("job: ", props.job);

const showFullDescription = ref(false);

const truncatedDescription = computed(()=> {
    let description = props.job.description;

    if(!showFullDescription.value){
        description = description.substring(0,90) + '...';
    }

    return description;
});

const toggleFullDescription = ()=>{
    showFullDescription.value = !showFullDescription.value
};

</script>

<template>
    <div class="card">
      <div class="card-content">
        <div class="job-info">
          <div class="job-type">{{ job.type }}</div>
          <h3 class="job-title">{{ job.title }}</h3>
        </div>
  
        <div class="job-description">
          <div>
            {{ truncatedDescription }}
          </div>
          <button @click="toggleFullDescription" class="toggle-description">
            {{ showFullDescription ? 'Less' : 'More' }}
          </button>
        </div>
  
        <h3 class="job-salary">{{ job.salary }} / Year</h3>
  
        <div class="divider"></div>
  
        <div class="job-footer">
          <div class="job-location">
            <i class="pi pi-map-marker"></i>
            {{ job.location }}
          </div>
          <RouterLink :to="'/jobs/' + job.id" class="read-more">
            Read More
          </RouterLink>
        </div>
      </div>
    </div>
  </template>
  
  <style scoped>
  .card {
    background-color: white;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    position: relative;
  }
  
  .card-content {
    padding: 16px;
  }
  
  .job-info {
    margin-bottom: 24px;
  }
  
  .job-type {
    color: #4a5568;
    margin-bottom: 8px;
  }
  
  .job-title {
    font-size: 1.25rem;
    font-weight: bold;
  }
  
  .job-description {
    margin-bottom: 20px;
  }
  
  .toggle-description {
    color: #10b981;
    background: none;
    border: none;
    cursor: pointer;
  }
  
  .toggle-description:hover {
    color: #059669;
  }
  
  .job-salary {
    color: #10b981;
    margin-bottom: 12px;
  }
  
  .divider {
    border-top: 1px solid #e5e7eb;
    margin-bottom: 20px;
  }
  
  .job-footer {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  
  .job-location {
    color: #c05621;
    margin-bottom: 12px;
  }
  
  .read-more {
    display: inline-block;
    height: 36px;
    background-color: #10b981;
    color: white;
    text-align: center;
    padding: 8px 16px;
    border-radius: 8px;
    text-decoration: none;
    font-size: 0.875rem;
  }
  
  .read-more:hover {
    background-color: #059669;
  }
  
  @media (min-width: 1024px) {
    .job-footer {
      flex-direction: row;
      align-items: center;
    }
  
    .job-location {
      margin-bottom: 0;
    }
  }
  </style>
  