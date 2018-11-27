<template>
  <div class="alert alert-primary">
    <h3>Правильные ответы: {{ stats.success }}</h3>
    <h3>Неправильные ответы: {{ stats.error }}</h3>
    <h5 v-if="stats.success != 3">Чтобы перейти на следующий уровень надо решить все примеры без ошибок!</h5>
    <h5 v-else>Молодец, Камилла! Ты можешь перейти на следующий уровень!!</h5>
    <hr>
    <button class="btn btn primary" @click="$emit('repeat')">Повторить</button>
    <button class="btn btn primary" @click="$emit('nextLevel')" v-if="stats.success == 3">Следующий уровень</button>
  </div>
</template>

<script>
  export default {
    props: ['stats']
  }
</script>

<style>

</style>
