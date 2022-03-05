<template>
  <div id="app">
  <div class="container" style="max-width: 600px">
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="w-100 form-control"
      />
    <button class="btn btn-warning rounded-0 mr-1" @click="start">Start</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="stop">Stop</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="reset">Reset</button>
    </div>

    <p>{{formattedElapsedTime}}</p>
  <table class="table table-bordered mt-5">
    <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">Duration</th>
        </tr>
      </thead>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>{{ task.name }}</td> 
      <td>{{task.duration}}</td>
    </tr>
    </table>
    </div>
  </div>
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