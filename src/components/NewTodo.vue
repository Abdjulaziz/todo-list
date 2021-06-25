<template>
  <form @submit.prevent="addTodo()" class="col-12 col-lf-6 addTodo">
    <input v-model="newTodo" placeholder="Enter Todo" type="text" class="form-control" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 1) {
        this.$emit('on-addtodo', this.newTodo);
      }
      this.newTodo = '';
    },
  },
};
</script>

<style lang="scss" scoped>
.addTodo{
  padding: 1rem 0;
}
</style>
