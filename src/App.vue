<template>
  <div class="container h-screen mx-auto flex justify-center items-center">
    <LayoutVue>
      <!-- Heder Component -->
      <template #header>
        <Header />
      </template>
      <!-- Composer -->
      <template #composer>
        <Composer v-model="title" @onAddTodo="addTodo" />
      </template>
      <!-- Filter -->
      <template #filter>
        <Filter
          :allTodo="allTodo"
          :pendingTodo="pendingTodo"
          :doneTodo="doneTodo"
          @onDdeleteTodos="deleteAllTodo"
          @onFiltered="filterMode=$event"
          :filterMode="filterMode"
        />
      </template>
      <!-- ToDos -->
      <template #todos>
        <Todo @click="todo.done=!todo.done" v-for="todo in filterTodos" :key="todo.id" :todo="todo" />
      </template>
    </LayoutVue>
  </div>
  <!-- Message -->
  <Message
    v-if="message.error.length > 0 || message.success.length > 0"
    :message="message"
  />
</template>

<script>
import LayoutVue from "./components/Layout.vue";
import Header from "./components/Header.vue";
import Composer from "./components/Composer.vue";
import Filter from "./components/Filter.vue";
import Todo from "./components/Todo.vue";
import { v4 as uuid } from "uuid";
import Message from "./components/Message.vue";

export default {
  components: {
    LayoutVue,
    Header,
    Composer,
    Filter,
    Todo,
    Message,
  },
  //* Component State
  data() {
    return {
      title: "",
      todos: [],
      message: {
        error: "",
        success: "",
      },
      filterMode: "all",
    };
  },
  // *Mounted
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  //* Component Methods
  methods: {
    addTodo() {
      if (this.title.length > 0) {
        let newTodo = {
          id: uuid(),
          title: this.title,
          done: false,
        };
        this.todos.unshift(newTodo);
        this.title = "";
        this.message.success = "ToDo Added";
        this.flashMessage();
        return;
      }
      (this.message.success = ""),
        (this.message.error = "Please Write Some Text First");
      this.flashMessage();
    },
    deleteAllTodo() {
      this.todos = [];
      localStorage.setItem("todos", this.todos);
    },
    flashMessage() {
      setTimeout(() => {
        this.message.error = "";
        this.message.success = "";
      }, 3000);
    },
 
  },
  //* Computed Property
  computed: {
    allTodo() {
      return this.todos.length;
    },
    pendingTodo() {
      return this.todos.filter((todo) => !todo.done).length;
    },
    doneTodo() {
      return this.todos.filter((todo) => todo.done).length;
    },

    filterTodos() {
      if (this.filterMode === "all") return this.todos;
      if (this.filterMode === "pending")
        return this.todos.filter((todo) => !todo.done);
      if (this.filterMode === "done")
        return this.todos.filter((todo) => todo.done);
    },
   
  },
  // *Watcher
  watch: {
    todos: {
      handler(newValue) {
        localStorage.setItem("todos", JSON.stringify(newValue));
      },
      deep: true,
    },
  },
};
</script>
