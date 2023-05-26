<script setup>
import { Icon } from '@iconify/vue';

const props = defineProps({
    todo: {
        type: Object,
        required: true,
    },
    index: {
      type: Number,
      required: true,
    }
})
defineEmits(['toggle-complete','edit-todo','update-todo','delete-todo'])
//console.log("TODO INFO: ", props.todo);
</script>

<template>
    <li>
        <input type="checkbox" :checked="todo.isCompleted" @input="$emit('toggle-complete', index)">
        <div class="todo">
            <input v-if="todo.isEditing" @input="$emit('update-todo', $event.target.value, index)" type="text" :value="todo.todo">
            <span v-else :class="{'completed-todo' : todo.isCompleted}">
                {{ todo.todo }}
            </span>
        </div>
        <div class="todo-actions">
            <Icon v-if="todo.isEditing" @click="$emit('edit-todo',index)" icon="ic:round-check-circle" class="icon" color="#4D61D2" width="22" />
            <Icon v-else icon="bxs:pencil" @click="$emit('edit-todo',index)" class="icon" color="#4D61D2" width="22" />
            <Icon icon="ion:trash" @click="$emit('delete-todo', todo.id)" class="icon" color="#f95e5e" width="22" />
        </div>
        <div>
          <Icon icon="ci:hamburger-md" class="hamburger-icon" color="#707070" width="22" />
        </div>
    </li>
</template>



<style lang="scss" scoped>
li {
  max-width: 500px;
  border-bottom: #979797 2px solid;
  display: flex;
  align-items: center;
  padding: 16px 10px;
  font-family: "Hind Vadodara";
 

  &:hover {
    border: none;
    border-radius: 10px;
    background-color: #fff;
    box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
    .todo-actions {
      opacity: 1;
    }
    .hamburger-icon{
      display: none;
    }
  }

  input[type="checkbox"] {
    position: relative;
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 15%;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);

    &:checked {
      content: "\2713";
      background-color: #4D61D2;
    }
    &:hover{
      cursor: pointer;
    }

    &:after {
      font-family: "Montserrat";
      content: "\2713";
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 14px;
      color: #fff;
    }
  }

  .todo {
    flex: 1;

    .completed-todo{
      text-decoration: line-through;
      opacity: 0.5;
    }

    input[type="text"] {
      width: 100%;
      border: 2px solid #4D61D2;
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
  .hamburger-icon{
      display: flex; 
  }
}
</style>