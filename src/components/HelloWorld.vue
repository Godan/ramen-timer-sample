<template>
  <v-container grid-list-md text-xs-center>
    <p class="font-bold text-3xl">{{ time }}</p>
    <div class="rounded w-full bg-gray-200 h-5 my-10">
      <div class="bg-blue-600 h-5 progressbar"></div>
    </div>
    <div row wrap>
      <div class="m-auto flex flex-row space-x-4 justify-center">
        <button
          class="rounded bg-sky-600 text-white px-5 py-2"
          @click="start()"
          v-show="!isRunning"
        >
          start
        </button>
        <button
          class="rounded bg-rose-600 text-white px-5 py-2"
          @click="stop()"
          v-show="isRunning"
        >
          stop
        </button>
        <button
          class="rounded bg-emerald-600 text-white px-5 py-2"
          @click="
            setTime();
            stop();
          "
          v-show="time != 180"
        >
          reset
        </button>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "HelloWord",
  data() {
    return {
      time: 10,
      isRunning: false,
      maxTime: 10,
      permissionGranted: false,
      pasent: 100,
    };
  },
  mounted() {},
  methods: {
    start() {
      this.isRunning = true;
      this.timer = setInterval(() => {
        if (this.isRunning && this.time > 0) {
          this.time--;
          this.pasent = `${(this.time / this.maxTime) * 100}%`;
          console.log(this.pasent);
        } else if (this.isRunning && this.time == 0) {
          this.timeOut();
        }
      }, 1000);
    },
    stop() {
      this.isRunning = false;
    },
    setTime() {
      this.time = this.maxTime;
      clearInterval(this.timer);
    },
    timeOut() {
      (async () => {})();
      this.isRunning = false;
    },
    calPasent() {
      const now = (this.time / this.maxTime) * 100;
      console.log(`${now} %`);
      return `${now} %`;
    },
  },
};
</script>

<style scoped>
.progressbar {
  width: v-bind("pasent");
}
</style>
