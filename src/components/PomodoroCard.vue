<script setup>
    import { ref, watch } from "vue";

    const props = defineProps({
    todo: {
        type: Object,
        required: true,
    },
    selectedTodo: {
        type: String,
        required: true,
    },
    });



    const currentSessions = ref(props.todo.currentSessions);
    const totalSessions = ref(props.todo.totalSessions);

    watch(props.todo,(newValue) => {
      currentSessions.value = props.todo.currentSessions
      totalSessions.value = props.todo.totalSessions
      
    }
    ,{deep:true});



    const updateCurrentSessions = (value) => {
      const savedTodoList = JSON.parse(localStorage.getItem("todoList"))
      currentSessions.value = Number(value);
   
      savedTodoList.forEach(todo => {
        if (todo.todo === props.todo.todo) {
         // console.log(todo.todo)
          todo.currentSessions = currentSessions.value;  
          localStorage.setItem("todoList", JSON.stringify(savedTodoList))
        }
      });

    };

    const updateTotalSessions = (value) => {
      const savedTodoList = JSON.parse(localStorage.getItem("todoList"))
      totalSessions.value = Number(value);
    
      savedTodoList.forEach(todo => {
        if (todo.todo === props.todo.todo) {
         // console.log(todo.todo)
          todo.totalSessions = totalSessions.value;
          localStorage.setItem("todoList", JSON.stringify(savedTodoList))
        }
      });
    };

   // console.log("TodoCard: ",props.todo.todo);
</script>



<template>
    <div :class="{'selectedCard': selectedTodo === todo.todo, 'card': selectedTodo !== todo.todo}">
      <h2>{{ todo.todo.length > 12 ? todo.todo.slice(0,12) : todo.todo }}</h2>
      <span>———————</span>
      <h3>YOU DID</h3>
      <div class="sessions">
        <input min="0" :value="currentSessions" type="number" @input="updateCurrentSessions($event.target.value)" />
        <span>/</span>
        <input min="0" :value="totalSessions" type="number" @input="updateTotalSessions($event.target.value)" />
      </div>
    </div>
</template>



<style lang="scss" scoped>
.sessions{
    margin-top: 10px;
    display: flex;
    flex-wrap: nowrap;

    input{
        -moz-appearance: textfield; /* Firefox */
        appearance: none;
        font-size: 1.7rem;
        width: 30px;
        border: none;
        border-radius: 10px;
        background-color: transparent;
        padding: 5px;
    }
    span{
        font-size: 2rem;
        margin:5px;
    }
}

.sessions input::-webkit-outer-spin-button,
.sessions input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
.card,
.selectedCard {
  border-radius: 15px;
  width: 175px;
  height: 250px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
    .sessions input{
        color: #fff;
    }
}

.card {
  color: #4d61d2;
  background-image: linear-gradient(to bottom right, #fff, #f0eeee);
  border-radius: 15px;
  width: 175px;
  height: 250px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
    .sessions input{
        color: #4d61d2;
    }
}

.selectedCard {
  color: #fff;
  background-image: linear-gradient(to bottom right, #5d6ecf, #4D61D2);
}

.card h2,
.selectedCard h2{
  margin: 0;
  font-family: "Hind Siliguri";
}
.card h3,
.selectedCard h3 {
  font-size: .8rem;
  margin: 0;
  font-family: "Hind Siliguri";
}
</style>