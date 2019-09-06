<template lang="pug">
  #app(@click="toggleTimerActive")
    .timer-wrapper
      .timer {{ countDownTime }}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class extends Vue {
  private restTime = 10 * 60
  public timerId: number | null = null

  public get countDownTime(): string {
    const minutes = Math.floor(this.restTime / 60)
    const seconds = this.restTime % 60
    return `${this.zeroPadding(minutes)}:${this.zeroPadding(seconds)}`
  }

  public toggleTimerActive() {
    if (!this.timerId) {
      this.timerId = setInterval(() => {
        if (this.restTime > 0) {
          this.restTime-- 
        }
      }, 1000)
    } else { 
      clearInterval(this.timerId)
      this.timerId = null
    }
  }

  private zeroPadding(s: number): string {
    return ('00' + s).slice(-2)
  }
}
</script>

<style lang="stylus">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body
  background-color #707070

.timer-wrapper
  display flex
  justify-content center
  align-items center
  height calc(100vh - 16px)
  width 100%

  color #ffffff
  font-size 512px

</style>
