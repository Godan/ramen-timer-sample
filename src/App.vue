<template>
  <div>
    <p class="flex justify-center font-bold text-3xl my-5">
      {{ convert_from_seconds_to_time(time) }}
    </p>
    <div class="rounded w-full bg-gray-200 h-5 my-10">
      <div
        class="bg-blue-600 h-5"
        v-bind:style="{ width: `${(this.time / this.maxTime) * 100}%` }"
      ></div>
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
  </div>
</template>

<script>
import "./index.css";

export default {
  name: "app",
  data() {
    return {
      time: 2,
      isRunning: false,
      maxTime: 2,
      permissionGranted: false,
      pasent: 100,
    };
  },

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
      this.isRunning = false;
      alert("時間です！");
    },
    convert_from_seconds_to_time(sec) {
      return `${Math.floor(sec / 60)}:${sec % 60}`;
    },
  },
};
</script>