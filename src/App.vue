<template>
    <TodoList />
</template>

<script>
import TodoList from './components/TodoList.vue';
export default {
  name: 'App',
  components: {
    TodoList,
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  transition: 0.3s;
}
body {
  background-color: #002841;
  color: #ffa500;
}

</style>
