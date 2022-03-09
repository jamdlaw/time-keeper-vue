<template>
  <div class="container" style="max-width: 600px">
    <div>
      <span>{{timer.days}}</span>:<span>{{timer.hours}}</span>:<span>{{timer.minutes}}</span>:<span>{{timer.seconds}}</span>
    </div>
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
import { useTimer } from 'vue-timer-hook';
export default defineComponent({
  name: "Home",
  setup() {
    const time = new Date();
    time.setSeconds(time.getSeconds() + 600); // 10 minutes timer
    const timer = useTimer(time);
    let tasks = [];
    const task = ref('');
    const stop = () => {
        tasks.push({  name: task,
                        duration: 0  
             });
        //timer.restart(0);
    }
  
    onMounted(() => {
      watchEffect(async () => {
        if(timer.isExpired.value) {
            console.warn('IsExpired')
        }
      })
    })
    return {
        timer,
        task : '',
        tasks, 
        stop
     };
  },
});
</script>