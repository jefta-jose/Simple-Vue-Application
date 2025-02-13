<script setup>

const props = defineProps({
    title: {
        type: String,
        default: 'Become A Vue Dev'
    },

    subtitle:{
        type: String,
        default: 'Find the Vue job that fits your skills and needs'
    }
});

</script>

<template>
  <section class="hero-section">
    <div class="container">
      <div class="text-center">
        <h1 class="hero-title">{{ title }}</h1>
        <p class="hero-subtitle">
            {{ subtitle }}
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  background-color: #2f855a; /* Equivalent to bg-green-700 */
  padding: 80px 0; /* Equivalent to py-20 */
  margin-bottom: 16px; /* Equivalent to mb-4 */
}

.container {
  max-width: 1280px; /* Equivalent to max-w-7xl */
  margin: 0 auto; /* Equivalent to mx-auto */
  padding: 0 16px; /* Equivalent to px-4 */
}

.text-center {
  text-align: center;
}

.hero-title {
  font-size: 2.5rem; /* Equivalent to text-4xl */
  font-weight: 800; /* Equivalent to font-extrabold */
  color: white; /* Equivalent to text-white */
}

@media (min-width: 640px) {
  .hero-title {
    font-size: 3rem; /* Equivalent to sm:text-5xl */
  }
}

@media (min-width: 768px) {
  .hero-title {
    font-size: 3.75rem; /* Equivalent to md:text-6xl */
  }
}

.hero-subtitle {
  margin-top: 16px;
  margin-bottom: 16px; /* Equivalent to my-4 */
  font-size: 1.25rem; /* Equivalent to text-xl */
  color: white;
}
</style>
