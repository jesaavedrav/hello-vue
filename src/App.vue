<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{greeting}}</h1>
    <!-- v-model -->
    <input class="m-2" v-model="greeting" />
    <button class="btn btn-dark m-2" @click="reverseString">Reverse</button>
    <h1 v-if="a===1">Show me just when a=1</h1>
    <h1 v-if="a===2">Show me just when a=2</h1>
    <h2>{{filterO}}</h2>
    <input class="m-2" v-model="newTodo.name" />
    <button class="btn btn-dark m-2" @click="addTodo(generateNewId, newTodo.name)">Add To Do</button>
    <b-list-group>
      <TodoItem v-for="item of todos" :key="item.id" :whateverthenameyoulike="item.name"></TodoItem>
    </b-list-group>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
export default {
  name: "App",
  data() {
    return {
      greeting: "Hello World",
      a: 111,
      todos: [
        { id: 1, name: "Learn how to use components" },
        { id: 2, name: "Learn how to pass data from parent to child" },
        { id: 3, name: "Learn how to bind a key" }
      ],
      newTodo: { id: 4, name: "" }
    };
  },
  components: {
    TodoItem
  },
  methods: {
    reverseString() {
      this.greeting = this.greeting
        .split("")
        .reverse()
        .join("");
    },
    addTodo(id, name) {
      this.todos.push({ id, name });
    }
  },
  computed: {
    filterO() {
      return this.greeting
        .split("")
        .filter(x => x != "o")
        .join("");
    },
    generateNewId() {
      var ids = this.todos.map(function(x) {
        return x.id;
      });
      let maxId = Math.max(...ids);
      return maxId + 1;
    }
  }
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
