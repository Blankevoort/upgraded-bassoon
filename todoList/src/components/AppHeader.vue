<template>
  <header class="card">
    <h1>لیست وظایف</h1>
    <button id="theme-switcher">
      <img :src="sunImage" alt="Change color theme" />
    </button>
  </header>
</template>

<script>
import Sun from '../assets/icon-sun.svg'
export default {
  name: 'AppHeader',
  data() {
    return {
      sunImage: Sun
    }
  }
}
</script>
