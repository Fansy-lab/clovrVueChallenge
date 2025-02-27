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
//add ref to todo, also it should be here up, not down between methods
const todos = ref([]);

//callApi should be an async function
// Lifecycle hooks (mounted here for easy access) ON TOP of script setup
onMounted(async () => {
  await callApi();
});

const reverseTextUtility = (text) => {
  return text.split("").reverse().join("");
};
const reverseTextOfElement = (id) => {
  //this is how you the function should look like
  const todo = todos.value.find((x) => x.id === id);
  todo.text = reverseTextUtility(todo.text);
};

const addTodo = () => {
  if (newTodo.value.length > 0) {
    // Add an id to the todo
    todos.value.push({ id: todos.value.length + 1, text: newTodo.value });
    newTodo.value = "";
  }
};

const removeTodo = (id) => {
  // this is how you remove an item from an array
  todos.value = todos.value.filter((x) => x.id !== id);
};

//this is how you should call an api, with try catch block
const callApi = async function () {
  try {
    const result = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    const json = await result.json();
    console.log(json);
  } catch (error) {
    console.log(error);
  }
};
</script>
<!-- add scoped -->
<style scoped>
button {
  background-color: blue;
  color: white;
  padding: 5px;
  margin: 5px;
  /* remove padding */
}
</style>
