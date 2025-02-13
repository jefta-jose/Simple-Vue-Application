<script setup>
import Card from './Card.vue';
</script>

<template>
    <!-- Developers and Employers -->
    <section class="section">
      <div class="container">
        <div class="grid">
        <Card>
            <div class="card card-developers">
                <h2 class="title">For Developers</h2>
                <p class="description">
                Browse our Vue jobs and start your career today
                </p>
                <RouterLink to="/jobs" class="button button-black">
                Browse Jobs
                </RouterLink>
            </div>
        </Card>

        <Card bg="background-color: #d1fae5;">
            <div class="card card-employers">
              <h2 class="title">For Employers</h2>
              <p class="description">
                List your job to find the perfect developer for the role
              </p>
              <RouterLink to="/jobs/add" class="button button-green">
                Add Job
              </RouterLink>
            </div>
        </Card>

        </div>
      </div>
    </section>
</template>

<style scoped>
.section {
  padding: 16px;
}

.container {
  max-width: 1200px;
  margin: auto;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
  padding: 16px;
  border-radius: 8px;
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: 1fr 1fr;
  }
}

.card {
  padding: 24px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

.title {
  font-size: 24px;
  font-weight: bold;
}

.description {
  margin: 8px 0 16px;
}

.button {
  display: inline-block;
  padding: 8px 16px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: bold;
}

.button-black {
  background-color: black;
  color: white;
}

.button-black:hover {
  background-color: #444;
}

.button-green {
  background-color: #22c55e;
  color: white;
}

.button-green:hover {
  background-color: #16a34a;
}
</style>
