<template>
  <div style="display: flex; flex-direction: column; height: 100%">
    <div style="margin-bottom: auto">
      <h1>{{ title }}</h1>
    </div>
    <div>
      <div style="border: 1px solid white">
        <h2>Todo List</h2>
        <input v-model="newTodo" placeholder="Add a new todo" />
        <button @click="addTodo">Add</button>
        <ul>
          <li v-for="todo in todos" :key="todo.id">
            {{ todo.text }}
            <button @click="reverseTextOfElement(todo.id)">Reverse Text</button>
            <button @click="removeTodo(todo.id)">Remove</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

const title = ref("Vue 3 Interview Challenge");
const message = ref("Hello Vue!");
const newTodo = ref("");

const reverseTextUtility = (text) => {
  return text.split("").reverse().join("");
};

const reverseTextOfElement = (id) => {
  //use the reverseTextUtility function to reverse the text
};

const addTodo = () => {
  if (newTodo.value.length > 0) {
    todos.value.push({ text: newTodo.value });
    newTodo.value = "";
  }
};

onMounted(() => {
  callApi();
});

const todos = [];
const removeTodo = (id) => {
  todos.value.splice(id, 1);
};

const callApi = function () {
  fetch("https://jsonplaceholder.typicode.com/todos/1")
    .then((response) => response.json())
    .then((json) => console.log(json));
};
</script>

<style>
button {
  background-color: blue;
  color: white;
  padding: 5px;
  margin: 5px;
  padding: 1px;
}
</style>
