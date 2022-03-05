<template>
  <div id="app">
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="w-100 form-control"
      />
    <button @click="start">Start</button>
    <button @click="stop">Stop</button>
    <button @click="reset">Reset</button>
    </div>

    <p>{{formattedElapsedTime}}</p>
  </div>
  <ul>
    <li v-for="(task, index) in tasks" :key="index">{{ task.name }} | {{task.duration}}</li>
  </ul>
</template>

<script>
import { nextTick } from 'vue'

export default {
  name: "App",
  data() {
    return {
      task: "",
      elapsedTime: 0,
      timer: undefined,
      tasks: []
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
      this.tasks.push({  name: this.task,
                        duration: this.formattedElapsedTime
             })
      clearInterval(this.timer);
    },
    reset() {
      this.elapsedTime = 0;
    }
  }

};
</script>