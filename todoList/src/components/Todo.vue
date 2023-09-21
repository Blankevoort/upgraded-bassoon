<template>
  <li class="card" draggable="true">
    <div class="cb-container">
      <input
        type="checkbox"
        :checked="todo.isComplete ? true : null"
        class="cb-input"
        @click="changeStatus"
      />
      <span class="check"></span>
    </div>
    <p class="item">{{ todo.title }}</p>
    <button class="clear" @click="deleteTodo">
      <img :src="crossImage" alt="Clear it" />
    </button>
  </li>
</template>

<script>
import Cross from '../assets/icon-cross.svg'
export default {
  props: {
    todo: Object
  },
  data() {
    return {
      crossImage: Cross
    }
  },
  methods: {
    deleteTodo() {
      if (confirm('آیا از حذف کار خود اطمینان دارید؟')) {
        this.$emit('Deleted', this.todo.id)
      }
    },
    changeStatus() {
      this.$emit('changeStatus', this.todo.id, !this.todo.isComplete)
    }
  }
}
</script>

<style></style>
