<script setup>
import TimerInput from './TimerInput.vue'
</script>
<script>
export default {
  data() {
    return {
      timerEnabled: 0,
      time: 0,
      timer: null,
      passed: 0,
    };
  },
  methods: {
    handleSubmit(totalSecs) {
      this.time = totalSecs
      this.timerEnabled = true;
      this.countDownTimer();
    },
    countDownTimer() {
      this.timer = setInterval(() => {
        // console.log((this.time / (this.time + this.passed)) * 100);
        this.time = this.time - 0.5;
        this.passed = this.passed + 0.5;
      }, 500);
    },
  },
  watch: {
    time: {
      handler(value) {
        if (value < 0) {
          this.timerEnabled = false;
          this.passed = 0;
          clearInterval(this.timer);
        }
      },
    },
  },
  computed: {
    timePercentage() {
      console.log("time", this.time);
      console.log("passed", this.passed);
      console.log((this.time / (this.time + this.passed)) * 100);
      return (this.time / (this.time + this.passed)) * 100;
    },
    minutesPrettify() {
      if (this.time / 60 <= 0) return "00";
      else if (this.time / 60 < 10)
        return "0" + String(Math.floor(this.time / 60));
      else return String(Math.floor(this.time / 60));
    },
  },
};
</script>

<template>
  <TimerInput v-if="!timerEnabled" @setTimer="handleSubmit"/>
  
  <div v-else>
    <!-- <span> {{ minutes }}:{{ secs }} </span> -->
    <div class="time-container" >
      <span class="time-minutes">{{ minutesPrettify }}</span>
      <span class="time-seconds">{{ Math.ceil(time % 60) }}</span>
    </div>

    <div class="progress-bar-container">
      <div class="progress-bar" :style="{ width: `${timePercentage}%` }"></div>
    </div>
  </div>
</template>

<style>
.form {
  padding: 1rem;
  display: flex;
  flex-wrap: wrap;
}
.input {
  padding: 0.5rem;
  width: 50%;
  font-size: 1.5rem;
  -webkit-appearance: none;
  -ms-appearance: none;
  -moz-appearance: none;
  appearance: none;
}
.input-submit {
  width: 100%;
}
.time-container {
  /* border:1px solid green; */
  text-align: center;
  font-size: 2.5rem;
}
.time-minutes::after {
  content: ":";
}

.progress-bar-container {
  /* border: 1px solid green; */
  width: 100%;
  border-radius: 1rem;
  overflow: hidden;
  border: 3px solid rgba(200, 200, 200, .7);
}
.progress-bar {
  border-radius: 1rem;
  transition: all 500ms linear;
  height: 3rem;
  background-color: rgba(160, 150, 150, .8);
}
</style>
