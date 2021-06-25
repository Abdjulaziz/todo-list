<template>
  <li class="d-flex justify-content-center list-group-item todo-list">
    <button
      v-if="!isEditing"
      :class="{ completed }"
      @click="$emit('on-toggle')"
      class="btn border-0 text-left flex-grow-1"
    >
      {{ todoString }}
    </button>
    <form v-else @submit.prevent="endEditing()" class="flex-grow-1">
      <input @blur="startEditing()" v-model="newTodoString" type="text" class="form-control" />
    </form>
    <button @click="startEditing()" class="btn btn-outline-primary"><i class="fas fa-edit"></i></button>
    <button @click="$emit('on-delete')" class="btn btn-outline-danger"><i class="fas fa-trash-alt"></i></button>
  </li>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    todoString: String,
    completed: Boolean,
  },
  data() {
    return {
      isEditing: false,
      newTodoString: '',
    };
  },
  methods: {
    startEditing() {
      if (!this.isEditing) {
        this.newTodoString = this.todoString;
        this.isEditing = true;
      } else {
        this.endEditing();
      }
    },
    endEditing() {
      this.isEditing = false;
      this.$emit('on-edit', this.newTodoString);
    },
  },
};
</script>

<style lang="scss" scoped>
.completed {
  text-decoration: line-through;
}
.todo-list{
  padding: 1rem 1rem;
  button{
    font-size: 1.5rem;
    text-align: left;
  }
  .fas{
    padding: 0 1rem;
  }
}
</style>
