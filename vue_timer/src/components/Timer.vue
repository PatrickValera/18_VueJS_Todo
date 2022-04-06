<script>
export default {
  data() {
    return {
      timerEnabled: 0,
      time: 0,
      minutes: 0,
      secs: 0,
    };
  },
  methods: {
    handleSubmit(e) {
      console.log(this.timerEnabled);
      this.timerEnabled = true;
    },
  },
};
</script>

<template>
  <div class="form" v-if="!timerEnabled">
    <form v-if="!timerEnabled" @submit.prevent="handleSubmit">
      <input v-model="minutes" type="number" placeholder="m" />
      <input v-model="secs" type="number" placeholder="s" />
      <input type="submit" value="submit" />
    </form>
  </div>
  <div v-else>
    <span> {{ minutes }}:{{ secs }} </span>
  </div>
</template>

<style></style>
