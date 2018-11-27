<template>
  <div id="training">
    <h3>Арифмитический тренажер для Камиллы!</h3>
    <hr>
    <div class="progress">
      <div class="progress-bar" :style="progrssStyles"></div>
    </div>
    <div class="box">
      <transition name="flip" mode="out-in">
        <app-start-screen
          v-if="state == 'start'"
          @onStart='onStart'
        ></app-start-screen>
        <app-question
          v-else-if="state == 'question'"
          @success="onQuestSuccess"
          @error="onQuestError"
          :settings="settings"
          :level="level"
        ></app-question>
        <app-message
          v-else-if="state == 'message'"
          :type="message.type"
          :text="message.text"
          @onNext="onNext"
        ></app-message>
        <app-result-screen
          v-else-if="state == 'result'"
          :stats="this.stats"
          @repeat="onStart"
          @nextLevel="onNextLevel"
        ></app-result-screen>
        <div v-else>Unknown state</div>
      </transition>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data() {
      return {
        state: 'start',
        stats: {
          success: 0,
          error: 0
        },
        message: {
          type: '',
          text: ''
        },
        questMax: 3,
        level: 0,
        settings:
          {
            from: 2,
            to: 10,
            range: Math.floor(Math.random() * 10),
            variants: 3,
          }
      }
    },
    computed: {
      questDone() {
        return this.stats.success + this.stats.error;
      },
      progrssStyles() {
        return {
          width: (this.questDone / this.questMax * 100) + '%'
        }
      }
    },
    methods: {
      onStart() {
        this.state = 'question';
        this.stats.success = 0;
        this.stats.error = 0;
      },
      onQuestSuccess() {
        this.state = 'message';
        this.message.text = 'Отлично Камилла! Все верно! Ты молодец!!! Продолжай в том же духе!';
        this.message.type = 'success';
        this.stats.success++;
      },
      onQuestError(msg) {
        this.state = 'message';
        this.message.text = msg;
        this.message.type = 'error';
        this.stats.error++;
      },
      onNext() {
        if (this.questDone < this.questMax) {
          this.state = 'question';
        } else {
          this.state = 'result';
        }

      },
      onNextLevel() {
        this.level++;
        this.settings.from += 2;
        this.settings.to += 2;
        this.settings.range += 1;
        if (this.settings.variants < 5) {
          this.settings.variants += 1;
        }
        this.onStart();
      }
    }
  }
</script>

<style scoped>
  #training {
    max-width: 700px;
    margin: 20px auto;
  }

  .progress-bar {
    transition: width 0.5s;
  }

  .box {
    margin: 10px 0;
  }

  .flip-enter {

  }

  .flip-enter-active {
    animation: flipInX 0.3s linear;
  }

  .flip-leave {

  }

  .flip-leave-active {
    animation: flipOutX 0.3s linear;
  }

  @keyframes flipInX {
    from {
      transform: rotateX(90deg)
    }
    to {
      transform: rotateX(0deg)
    }
  }

  @keyframes flipOutX {
    from {
      transform: rotateX(0deg)
    }
    to {
      transform: rotateX(90deg)
    }
  }
</style>
