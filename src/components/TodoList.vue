<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <p class="display-3">Enter task</p>
      </div>
    </div>
    <div class="row">
      <div class="col col-lg-12">
        <NewTodo @on-addtodo="addTodo($event)" />
      </div>
    </div>
    <div class="row">
      <div class="col-12 col-lg-12">
        <ul class="list-group">
          <Todo
            v-for="(todo, index) in todos"
            :key="index"
            :todoString="todo.todoString"
            :completed="todo.completed"
            @on-delete="deleteTodo(todo)"
            @on-toggle="toggleTodo(todo)"
            @on-edit="editTodo(todo, $event)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import NewTodo from './NewTodo';
import Todo from './Todo.vue';
export default {
  components: {
    Todo,
    NewTodo,
  },
  name: 'TodoList',
  data() {
    return {
      todos: [],
    };
  },
  beforeMount() {
    localStorage.getItem('todos') != null
      ? (this.todos = JSON.parse(localStorage.getItem('todos')))
      : (this.todos = []);
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({
        todoString: newTodo,
        completed: false,
      });
      this.saveLocalStorage();
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    editTodo(todo, newTodoString) {
      todo.todoString = newTodoString;
    },
    deleteTodo(deleteTodo) {
      this.todos = this.todos.filter((todo) => todo.todoString !== deleteTodo.todoString);
      this.saveLocalStorage();
    },
    saveLocalStorage() {
      let jsonTodos = JSON.stringify(this.todos);
      localStorage.setItem('todos', jsonTodos);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
