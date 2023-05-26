<script setup>
import PomodoroCard from './PomodoroCard.vue';


const props = defineProps({
    sharedListItems: {
        type: Array,
        required: true,
    },
    selectedTodo: {
        type: String,
        required: true,
        default: ()=> ""
    }

  
})

/* watch(props.sharedListItems,(newValue) => {
 
  props.sharedListItems=newValue
  console.log("PomodoroCardGrid: ", props.sharedListItems)
}
,{deep:true}); */


</script>



<template>
    <div class="cards">
        <PomodoroCard v-for="todo in sharedListItems" :todo="todo" :selectedTodo="selectedTodo"></PomodoroCard>
    </div>
</template>



<style lang="scss" scoped>
.cards{
    width: 100%;
    margin-top: 5rem;
    align-items: center;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(185px, 1fr));
    row-gap: 1rem;
    justify-items: center;
    //max-width: 740px;
}
</style>