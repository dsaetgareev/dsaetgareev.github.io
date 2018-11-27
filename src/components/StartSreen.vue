<template>
  <div class="alert alert-secondary">
    <h3>Попробуй решить примеры.</h3>
    <h3>Камилла, ты готова?</h3>
    <button class="btn btn-success" @click="$emit('onStart')">Начинай!</button>
  </div>
</template>

<script>
  export default {
    methods: {

    }
  }

</script>

<style scoped>
  .alert{
    text-align: center;
  }
  h3, .btn{
    margin:  30px 0;
  }
</style>
