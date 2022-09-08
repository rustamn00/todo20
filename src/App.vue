<script setup>
import { ref, computed } from "vue";

const msg = ref("Hello World!");
const todos = ref([]);
let aa = ref("");

const content_info = ref("");
const category = ref(null);

const addItem = () => {
  todos.value.push({
    info: content_info.value,
    category: category.value,
    date: new Date().getTime(),
  });
  content_info.value = "";
  category.value = "";
  console.log(todos);
};

const todo_asc = () =>
  todos.value.sort((a, b) => {
    return a.date - b.date;
  });

const remove = (todo) => {
  todos.value = todos.value.filter((a) => a !== todo);
};
</script>

<template>
  <form @submit.prevent="addItem">
    <input v-model="content_info" type="text" />
    <label>
      <input type="radio" name="category" value="personal" v-model="category" />
      <span>Personal</span>
    </label>
    <label>
      <input type="radio" name="category" value="business" v-model="category" />
      <span>Business</span>
    </label>
    <input type="submit" value="Add todo" />
  </form>
  <div v-for="todo in todos">
    <h1>{{ todo.category }}</h1>
    <input class="info" type="text" v-model="todo.info" />
    <button @click="remove(todo)">Remove</button>
  </div>
  {{ todo_asc }}
</template>

<style>
.info {
  border: 0;
}
</style>
