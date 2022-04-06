<script>
export default {
  data() {
    return {
      timerEnabled: 0,
      time: 0,
      minutes: 0,
      secs: 0,
      timer: null,
      passed: 0,
    };
  },
  methods: {
    handleSubmit(e) {
      this.time = this.minutes * 60 + this.secs;
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
  <div  v-if="!timerEnabled">
    <form class="form" v-if="!timerEnabled" @submit.prevent="handleSubmit">
      <input class='input' v-model="minutes" type="number" placeholder="m" />
      <input class='input' v-model="secs" type="number" placeholder="s" />
      <input class='input input-submit' type="submit" value="submit" />
    </form>
  </div>
  <div v-else>
    <!-- <span> {{ minutes }}:{{ secs }} </span> -->
    <div class="time-container">
      <span class="time-minutes">{{ minutesPrettify }}</span>
      <span class="time-seconds">{{ Math.ceil(time % 60) }}</span>
    </div>

    <div class="progress-bar-container">
      <div class="progress-bar" :style="{ width: `${timePercentage}%` }"></div>
    </div>
  </div>
</template>

<style>

.form{
    padding: 1rem;
    display: flex;
    flex-wrap: wrap;

}
.input{
    padding:.5rem;
    width: 50%;
    font-size: 1.5rem;
}
.input-submit{
    width: 100%;
}
.time-container{
    /* border:1px solid green; */
    text-align: center;
    font-size: 2rem;
}
.time-minutes::after{
    content:":"
}

.progress-bar-container {
  /* border: 1px solid green; */
  width: 100%;
  border-radius: 1rem;
  overflow: hidden;
  border:3px solid white;

}
.progress-bar {
  border-radius: 1rem;
  transition: all 500ms linear;
  height: 2rem;
  background-color: #555;
}
</style>
