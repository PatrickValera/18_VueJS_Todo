<script>
export default {
  data() {
    return {
      minutes: null,
      seconds: null,
    };
  },
  methods: {
    handleSubmit() {
      console.log("hello");
      this.$emit("setTimer", this.minutes * 60 + this.seconds);
    },
  },
};
</script>

<template>
  <div>
    <form class="form" @submit.prevent="handleSubmit">
      <input class="input" v-model="minutes" type="number" placeholder="m" />
      <input class="input" v-model="seconds" type="number" placeholder="s" />
      <input class="input input-submit" type="submit" value="submit" />
    </form>
  </div>
</template>



<style>
.form {
    position: fixed;
    bottom:0;
    width: 100%;
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
</style>