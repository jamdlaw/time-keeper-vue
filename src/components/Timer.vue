<template>
  <div class="container" style="max-width: 600px">
     <input
        type="text"
        placeholder="Enter task"
        v-model="task"
        class="w-100 form-control"
      />
    <p>{{timer.isRunning ? 'Running' : 'Not running'}}</p>
    <button class="btn btn-warning rounded-0 mr-1"  @click="timer.start()">Start</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="timer.pause()">Pause</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="timer.resume()">Resume</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="stop()">Stop</button>
  </div>
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
</template>
<script>
import { defineComponent, watchEffect, onMounted, ref } from "vue";
export default defineComponent({
  name: "Home",
  setup() {
    let tasks = [];
    const task = ref('');
    const stop = () => {
        tasks.push({  name: task,
                        duration: 0  
             });
    }
  
    return {
        task : '',
        tasks, 
     };
  },
});
</script>