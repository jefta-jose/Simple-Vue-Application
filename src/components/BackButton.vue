<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
  <section>
    <div class="container">
      <RouterLink to="/jobs" class="back-link">
        <i class="pi pi-arrow-circle-left icon"></i> Back to Job Listings
      </RouterLink>
    </div>
  </section>
</template>

<style>
.container {
  max-width: 1200px;
  margin: auto;
  padding: 24px;
}

.back-link {
  color: #16a34a; /* Green-500 */
  text-decoration: none;
  display: flex;
  align-items: center;
  transition: color 0.2s ease-in-out;
}

.back-link:hover {
  color: #15803d; /* Green-600 */
}

.icon {
  margin-right: 12px;
}
</style>
