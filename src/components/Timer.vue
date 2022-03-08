<template>
  <div class="container" style="max-width: 600px">
    <div>
      <span>{{timer.days}}</span>:<span>{{timer.hours}}</span>:<span>{{timer.minutes}}</span>:<span>{{timer.seconds}}</span>
    </div>
     <input
        type="text"
        placeholder="Enter task"
        class="w-100 form-control"
      />
    <p>{{timer.isRunning ? 'Running' : 'Not running'}}</p>
    <button class="btn btn-warning rounded-0 mr-1"  @click="timer.start()">Start</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="timer.pause()">Pause</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="timer.resume()">Resume</button>
    <button class="btn btn-warning rounded-0 mr-1" @click="timer.restart(0)">Stop</button>
  </div>
</template>
<script>
import { defineComponent, watchEffect, onMounted } from "vue";
import { useTimer } from 'vue-timer-hook';
export default defineComponent({
  name: "Home",
  setup() {
    const time = new Date();
    time.setSeconds(time.getSeconds() + 600); // 10 minutes timer
    const timer = useTimer(time);
    
    onMounted(() => {
      watchEffect(async () => {
        if(timer.isExpired.value) {
            console.warn('IsExpired')
        }
      })
    })
    return {
        timer,
        
     };
  },
});
</script>