<script setup>
import Pomodoro from '../components/Pomodoro.vue'
import TodoBlock from '../components/TodoBlock.vue';
import { ref } from "vue";

const sharedListItems = ref([]);

const updateTodoList = (newList) => {
  sharedListItems.value = newList
  //console.log("UPDATED SHARED-List: ",sharedListItems.value);

}
</script>


<template>
  <main class="home">
    <TodoBlock @updateTodoList="updateTodoList" />
    <Pomodoro :sharedListItems="sharedListItems"/>
    
  </main>
</template>

<style lang="scss" scoped>
.home {
  width: 100%;
  display: grid;
  grid-template-columns: minmax(200px, 1fr) minmax(400px, 2fr);
  align-items: center;
  //height: 100vh;
  background-color: #fff;

  @media (max-width: 1300px) {
    grid-template-columns: 1fr;
  }
}


</style>