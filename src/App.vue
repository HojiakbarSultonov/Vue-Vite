<template>
  <div>
    <h1>Counter: {{ counter }}</h1>
    <div class="d-flex">
      <button v-on:click="onIncrement" class="btn btn-success" >Add</button>
      <button class="btn btn-danger"  v-on:click="onDecrement">Delete</button>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      counter:0
    }
  },
  methods:{
    onIncrement(){
      this.counter += 1
    },
    onDecrement(){
      this.counter -= 1
    },
  }
}
</script>
<style></style>
