<template>
  <div class="container">
    <h1>Todo List</h1>
    <div v-if="!isEditing">
      <input type="text" v-model="todo" />
      <input type="submit" value="add" @click="storeTodo" />
    </div>

    <div v-else>
      <input type="text" v-model="todo" />
      <input type="submit" value="update" @click="updateTodo" />
    </div>

    <ol class="ol">
      <li v-for="(todo, index) in todos" :key="todo">
        {{ todo }}

        <button @click="editTodo(index, todo)" class="edit">Edit</button>
        <button @click="deleteTodo(index)" class="delete">Delete</button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  data() {
    const isEditing = false;
    const selectedIndex = null;
    const todo = "";
    const todos = [];
    return {
      todo,
      todos,
      selectedIndex,
      isEditing,
    };
  },
  methods: {
    storeTodo() {
      this.todos.push(this.todo);
      this.todo = "";
    },
    editTodo(index, todo) {
      this.todo = todo;
      this.selectedIndex = index;
      this.isEditing = true;
    },
    updateTodo() {
      this.todos.splice(this.selectedIndex, 1, this.todo);
      this.isEditing = false;
      this.todo = "";
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
.edit {
  margin: 0 10px;
}
</style>
