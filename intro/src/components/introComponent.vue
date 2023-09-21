<template>
  <div>
    <h1 @click="alert()">full name: {{ name }} {{ family }}</h1>
    <p>age: {{ age }}</p>
    <p>phone number: {{ phone }}</p>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    family: String,
    age: Number,
    phones: Array
  },
  methods: {
    alert() {
      alert(this.name)
      this.$emit('nameClicked', this.name + ' ' + this.family)
    }
  }
}
</script>

<style scoped>
h1 {
  color: red;
}
</style>
