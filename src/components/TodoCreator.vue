
<script setup>
import { reactive } from "vue";


const todoState = reactive({
    todo: "",
    invalid: false,
    errMsg: ""
});
const emit = defineEmits(["create-todo"])

const createTodo = () => {
    todoState.invalid = false;
    if (todoState.todo !=="") {
        emit('create-todo', todoState.todo);
        todoState.todo="";
        return;
    }
    todoState.invalid = true;
    todoState.errMsg = "Todo value cannot be empty";
}
</script>


<template>
    <div class="input-wrap" :class="{ 'input-err' :  todoState.invalid}">
        <input placeholder="Add a todo" class="input" type="text" v-model="todoState.todo">
        <button @click="createTodo()" class="btn">Add</button>
    </div>
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>


<style lang="scss" scoped>
.input-wrap {
  font-family: "Hind Vadodara";
  display: flex;
  gap: 10px;
  max-width: 500px; /* Agregar borde inferior */
  margin-bottom: 10px; /* Ajustar margen inferior */
}

.input {
  font-family: "Hind Vadodara";
  background-color: #fafafa;
  flex: 1; /* Ajustar ancho del input al resto del espacio disponible */
  border: none;
  border-bottom: 2px solid #979797; /* Quitar bordes del input */
  outline: none; /* Quitar el contorno de enfoque */
  &:hover{
    caret-color: black !important;
  }
}


.input-err {
  font-family: "Hind Vadodara";
  display: flex;
  border: 2px solid red;
}

.btn {
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

.err-msg {
  color: red;
  margin-top: 5px; /* Ajustar margen superior */
}
</style>