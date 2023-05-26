<script setup>
import Clock from '../components/Clock.vue'
import PomodoroCardGrid from './PomodoroCardGrid.vue';
import { Icon } from '@iconify/vue';
import { ref, watch } from "vue";
import alert from '../assets/sounds/alert.mp3';

const props = defineProps({
    sharedListItems: {
        type: Array,
        required: true,
        default: () => []
    },
})

const localStorageList = ref([])

function getLocalStorageTodos () {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"))
    //console.log("SHAREDLIST: ",props.sharedListItems.value);
    if (props.sharedListItems.length === 0) {
        localStorageList.value = savedTodoList
        //console.log("LOCALSTORAGELIST: ",localStorageList.value)
    }
}

getLocalStorageTodos();

const selectedTodo = ref("");

//timer logic
const time = ref(5); // 25 minutos en segundos 1500
const isRunning = ref(false);
let timer;



function startTimer() {
  isRunning.value = true;
  timer = setInterval(() => {
    time.value--;
    if (time.value === 0) {
      stopTimer();
      handleResetTime();
      //playAudio();
      const audio = new Audio(alert);
      audio.play();
      //add +1 to todo.currentSessions
      //console.log("SEELECTED: ",selectedTodo.value);
      //localStorageList.value = SON.parse(localStorage.getItem("todoList"))
      if(selectedTodo != ""){
        localStorageList.value.forEach((todo)=>{
          //console.log(todo.todo);
          if (todo.todo === selectedTodo.value) {
            todo.currentSessions ++;
            //console.log("innerLocalStorage: ",localStorageList.value)
          }
        })
        props.sharedListItems.forEach((todo)=>{
          //console.log("sharedList", todo)
          if (todo.todo === selectedTodo.value) {
            todo.currentSessions ++;
           // console.log("innerPROPS: ",props.sharedListItems)
          }
        })
      }
    }
  }, 1000);
}

watch(localStorageList,(newValue) => {
  localStorage.setItem("todoList", JSON.stringify(localStorageList.value))
  localStorageList.value=newValue
}
,{deep:true});

function stopTimer() {
  isRunning.value = false;
  clearInterval(timer);
}

function handleButtonClick() {
  if (isRunning.value) {
    stopTimer();
  } else {
    startTimer();
  }
}

function handleResetTime(){
  stopTimer();
  isRunning.value=false;
  time.value=5;
}

function formatTime(time) {
  const minutes = Math.floor(time / 60);
  const seconds = time % 60;
  return `${padTime(minutes)}:${padTime(seconds)}`;
}

function padTime(value) {
  return value.toString().padStart(2, '0');
}

</script>

<template>
    <div class="pomodoro">
        <h2 class="title">pomodoro</h2>
        <div class="clockBlock">
            <Clock :time="formatTime(time)"/>
            <div class="rightBlock">
                <h1><span>|</span> KEEP GOING</h1>
                <div class="alarm">
                    <Icon icon="clarity:notification-solid" width="14" color="#4D61D2"/>
                    <p>Select your todo</p>
                </div>
                <select v-model="selectedTodo">
                    <option v-if="localStorageList.length > 0 & props.sharedListItems.length === 0" v-for="todo in localStorageList">{{todo.todo}}</option>
                    <option v-else v-for="todo in sharedListItems">{{todo.todo}}</option>    
                </select>
                <div class="buttons">
                  <button class="btn" @click="handleButtonClick">{{ isRunning ? 'Pause' : 'Start' }}</button>
                  <button class="reset-btn" @click="handleResetTime">
                    <Icon icon="carbon:reset" />
                  </button>
                </div>
            </div>
        </div>
        <div class="cardsGrid">
            <PomodoroCardGrid v-if="localStorageList.length > 0 & props.sharedListItems.length === 0" :sharedListItems="localStorageList" :selectedTodo="selectedTodo"></PomodoroCardGrid>
            <PomodoroCardGrid v-else :sharedListItems="props.sharedListItems" :selectedTodo="selectedTodo"></PomodoroCardGrid>
        </div>
       
    </div>
</template>



<style lang="scss" scoped>
.pomodoro{
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;
    height: 100%;
    width: 100%;
    background-color: #F1F1F1;
}
.title{
    padding-left: 3rem;
    align-self: flex-start;
    margin-top: 3rem;
    color: #707070;
    font-family: "Montserrat Alternates";
}

.clockBlock{
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 1.5rem;
    justify-content: center;

    h1{
    font-family: "Hind Siliguri";
    margin-bottom: 0;
    color: #707070;
    font-weight: 700;
    font-size: 2rem;
    color: #4D61D2;
    }
    
    span{
        color: #4D61D2;
    }

    .rightBlock{
        display: flex;
        flex-direction: column;

        .alarm{
            font-family: "Hind Siliguri";
            color: #4D61D2;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        select{
          background-color: #aeaeae;
          border-radius: 5px;
          font-size: 1.2rem;
          border: none;
          padding: 5px;
          color: #FAFAFA;
        }
    }

}
.buttons{
  display: flex;
  gap: 5px;
}

.btn {
  width: 100%;
  margin-top: 2rem;
  background-color: #4D61D2;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  cursor: pointer;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
  &:hover{
    background-color: #4051af;
  }
}

.reset-btn{
  margin-top: 2rem;
  background-color: #aeaeae;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  cursor: pointer;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
  &:hover{
    background-color: #8d8b8b;
  }
}

.cardsGrid{
    width: 100%;
    max-width: 750px;
}

</style>