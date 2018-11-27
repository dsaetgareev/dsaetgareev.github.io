<template>
  <div>
    <div class="alert">
      <h3>{{ x }} + {{ y }} = ?</h3>
      <div class="buttons">
        <button class="btn btn-success"
                v-for="number in answers"
                @click="onAnswer(number)"
        >
          {{ number }}
        </button>
      </div>
    </div>
    <span class="level">Уровень  {{ level + 1 }}.</span>
  </div>
</template>

<script>
  export default {
    props: ['settings', 'level'],
    data() {
      return {
        x: mtRand(this.settings.from, this.settings.to),
        y: mtRand(this.settings.from, this.settings.to)
      }
    },
    computed: {
      good() {
        return this.x + this.y;
      },
      answers() {
        let res = [this.good];
        while (res.length < this.settings.variants) {
          let num = mtRand(this.good - this.settings.range, this.good + this.settings.range);
          if (res.indexOf(num) === -1) {
            res.push(num);
          }
        }
        return res.sort(function () {
          return Math.random() - 0.5;
        });
      }
    }, methods: {
      onAnswer(num) {
        if (this.good === num) {
          this.$emit('success');
        } else {
          this.$emit('error', `Нет, Камиллочка! \t Ответ: ${this.x} + ${this.y} = ${this.good}!`)
        }
      }
    }
  }

  function mtRand(min, max) {
    let diff = max - min;
    return Math.floor(Math.random() * (diff + 1)) + min;
  }
</script>

<style>
  .alert {
    text-align: center;
    padding-top: 20px;
    background-color: #eee;
  }

  .buttons {
    display: flex;
    justify-content: space-around;
  }

  .btn {
    margin: 20px 0;
  }

  .level {
    text-align: left;
  }
</style>
