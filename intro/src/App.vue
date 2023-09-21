<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <introComponent :name="name" :family="family" :age="age" :phone="phone" @nameClicked="Log" />
  </main>
</template>

<script>
import { ref, watch } from 'vue'
import introComponent from './components/introComponent.vue'

export default {
  components: {
    introComponent
  },

  setup() {
    const name = ref('Moeen')
    const family = ref('Sedaqati')
    const age = ref('16')
    const phone = ref('09379608155')

    function Log(data) {
      console.log(data)
    }

    return {
      name,
      family,
      age,
      phone,
      Log
    }
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
