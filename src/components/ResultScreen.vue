<template>
  <div class="alert alert-primary">
    <h3>Правильные ответы: {{ stats.success }}</h3>
    <h3>Неправильные ответы: {{ stats.error }}</h3>
    <h5 v-if="stats.success != 3">
      <p>Чтобы перейти на следующий уровень надо решить все примеры без ошибок!</p>
      <p>Реши все задачи правильно и получишь приз!!!</p>
    </h5>
    <h5 v-else>
      <p>Молодец, Камилла! Ты можешь перейти на следующий уровень!!</p>
      <p>Ты хорошо потрудилась, теперь можешь отдохнуть и посмотреть этот познавательный фильм.</p>
    </h5>
    <hr>
    <button class="btn btn primary" @click="$emit('repeat')">Повторить</button>
    <div v-if="stats.success == 3">
      <button class="btn btn primary" @click="$emit('nextLevel')">Следующий уровень</button>
      <youtube :video-id="videoList[getId]" @ready="ready"></youtube>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['stats'],
    data() {
      return {
        videoId: 'iI5O0q744io',
        videoList:['BctpoqOJuns', 'iI5O0q744io', '7ZRJ8LCi0kU', 'pzOYsFg1dxo', 'tBPpBA8qgCE',
        'wg6jh2aY27Q', 'bKOFZSz1sTY', 'KG6Teen3TQc', 'dxm4jiW4vFU', 'fbkDsG7ldOQ', 'vX9OieONxQA', 'oQ7zwmHnF9c',
        'xCVNgM-vJ88', 'ytyOELXZ4GU', 'waszCOR-tc4', '29nL91xdfMY', '0JW2-NxquA8', 'gc7_wRV7w9w',
        'Qg0ACKG8yq0', 'PLcUOA4FFMK6Os4O89ScOGO8jl13T-n1Bv']
      }
    },
    computed: {
      getId() {
        return Math.floor(Math.random() * this.videoList.length)
      }
    },
    methods: {
      ready(event) {
        this.player = event.player
      },
    },
  }
</script>

<style>

</style>
