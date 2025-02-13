<script setup>
import { RouterLink, useRoute } from 'vue-router';

const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
}

</script>


<template>
  <nav class="navbar">
    <div class="container">
      <div class="nav-content">
        <div class="nav-left">
          <!-- Logo -->
          <RouterLink class="logo" to="/">
            
            <span class="logo-text">Vue Jobs</span>
          </RouterLink>
          <div class="nav-links">
            <RouterLink to="/" class="nav-link active">Home</RouterLink>
            <RouterLink to="/jobs" class="nav-link">Jobs</RouterLink>
            <RouterLink to="/jobs/add" class="nav-link">Add Job</RouterLink>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
/* Navbar styles */
.navbar {
  background-color: #2f855a;
  border-bottom: 2px solid #276749;
  padding: 10px 0;
}

/* Container */
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Navbar content */
.nav-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 80px;
}

/* Logo */
.logo {
  display: flex;
  align-items: center;
  text-decoration: none;
}

.logo-img {
  height: 40px;
  width: auto;
}

.logo-text {
  display: none;
  color: white;
  font-size: 24px;
  font-weight: bold;
  margin-left: 10px;
}

@media (min-width: 768px) {
  .logo-text {
    display: block;
  }
}

/* Navigation links */
.nav-links {
  display: flex;
  margin-left: auto;
}

.nav-link {
  color: white;
  text-decoration: none;
  padding: 10px 15px;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.nav-link:hover {
  background-color: #22543d;
}

.nav-link.active {
  background-color: #22543d;
}

.nav-left{
  width: 100%;
  display:  flex;
}
</style>
