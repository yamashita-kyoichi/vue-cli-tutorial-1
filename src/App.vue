<template>
  <div id="app">
    <h1>簡易TODOアプリ</h1>
    <input v-model="message" />
    <button :disabled="isDisabled" @click="add">追加</button>
    <br />
    <div v-if="todos.length === 0">タスクはありません</div>
    <div v-else>
      <ul>
        <TaskCard
          v-for="todo in todos"
          :id="todo.id"
          :key="todo.id"
          :text="todo.text"
          @remove-task="remove"
        />
      </ul>
    </div>
  </div>
</template>


<script>
import TaskCard from "./components/TaskCard";

export default {
  name: "App",
  components: {
    TaskCard,
  },
  data: () => ({
    message: "Spark joy!",
    todos: [
      { id: 1, text: "ときめき" },
      { id: 2, text: "メモリアル" },
    ],
  }),
  methods: {
    onInput(event) {
      const text = event.target.value;
      this.message = text;
    },
    add() {
      const newTodo = {
        id: this.todos.length + 1,
        text: this.message,
      };
      this.todos.push(newTodo);
      this.message = "";
    },
    remove(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
  computed: {
    isDisabled() {
      return this.message.length === 0;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
