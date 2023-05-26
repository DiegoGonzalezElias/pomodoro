<script setup>
import {ref} from "vue";
import TodoCreator from './TodoCreator.vue';
import TodoItem from "./TodoItem.vue";
import {uid} from "uid";


const todoList = ref([]);

const fetchTodoList = () => {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"))
    if (savedTodoList) {
        todoList.value = savedTodoList;
    }
}

fetchTodoList();

const setTodoListLocalStorage = () => {
    localStorage.setItem("todoList", JSON.stringify(todoList.value))
};

const emit = defineEmits(["updateTodoList"])

const createTodo = (todo) =>{
    todoList.value.push({
        id:uid(),
        todo,
        isCompleted: false,
        isEditing: false,
        currentSessions: 0,
        totalSessions: 0
    });
    setTodoListLocalStorage();
    emit("updateTodoList",todoList.value);
}


const toggleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
    setTodoListLocalStorage();
    emit("updateTodoList",todoList.value);
}

const toggleEditTodo = (todoPos) => {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing
    setTodoListLocalStorage();
    emit("updateTodoList",todoList.value);
}

const updateTodo = (todoVal, todoPos) => {
    todoList.value[todoPos].todo = todoVal;
    setTodoListLocalStorage();
    emit("updateTodoList",todoList.value);
}

const deleteTodo = (todoId) => {
    todoList.value = todoList.value.filter((todo) => todo.id !==todoId)
    setTodoListLocalStorage();
    emit("updateTodoList",todoList.value);
}

//console.log("TODOLIST: ", todoList)
</script>

<template>
    <div class="todoBlock">
        <h2 class="title">toDo List</h2>
        <TodoCreator @create-todo="createTodo"/>
        <ul v-if="todoList.length > 0" class="todoList">
            <TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" 
            @toggle-complete="toggleTodoComplete" 
            @edit-todo="toggleEditTodo"
            @update-todo="updateTodo"
            @delete-todo="deleteTodo"/>
        </ul>
        <p v-else class="todos-msg">
            You have no todos to complete! Add one!
        </p>
    </div>
</template>



<style lang="scss" scoped>
.todoBlock{
    background-color: #fafafa;
    padding: 0 3rem 0 3rem;
    height: 100%;

}
.title{
    margin-top: 3rem;
    color: #707070;
    font-family: "Montserrat Alternates";
}

.todoList{
    padding: 0;
}
</style>