<template>
  <div id="app">
    <button @click="start">Start</button>
    <button @click="stop">Stop</button>
    <button @click="reset">Reset</button>
    <p>{{formattedElapsedTime}}</p>
  </div>
</template>

<script>
import { nextTick } from 'vue'

export default {
  name: "App",
  data() {
    return {
      elapsedTime: 0,
      timer: undefined
    };
  },
  computed: {
    formattedElapsedTime() {
      const date = new Date(null);
      date.setSeconds(this.elapsedTime / 1000);
      const utc = date.toUTCString();
      return utc.substr(utc.indexOf(":") - 2, 8);
    }
  },
  methods: {
   async start() {
      this.timer = setInterval(() => {
        this.elapsedTime += 1000;
      }, 1000);
       await nextTick()
      // DOM is now updated
      document.title = this.formattedElapsedTime;
    },
    stop() {
      clearInterval(this.timer);
    },
    reset() {
      this.elapsedTime = 0;
    }
  }

  //updated() {
   //   console.log('updated!')
   // }
};
</script>