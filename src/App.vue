<template>
  <div class="app">
    <div class="inner">
      <NewTodo @addTodo="addTodo"></NewTodo>
      <TodoList :list="list" @updateTodo="updateTodo"></TodoList>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Mixins } from 'vue-property-decorator';
import NewTodo from './components/NewTodo.vue';
import TodoList from './components/TodoList.vue';
import Todo from './models/Todo';

@Component({
  components: {
    NewTodo,
    TodoList,
  },
  watch: {
    list(newValue: Array<Todo>) {
      console.log('我开始存储TodoList数据了');
      let string = JSON.stringify(newValue);
      localStorage.setItem('data', string);
    },
  },
})
export default class App extends Vue {
  list: Array<Todo> = localStorage.getItem('data') ? JSON.parse(<string>localStorage.getItem('data')) : [];
  addTodo(name: String) {
    let todo: Todo = { name: name, status: 'todo' };
    this.list.push(todo);
  }
  updateTodo(todo: Todo, part: Partial<Todo>) {
    let index: number = this.list.indexOf(todo);
    let newTodo: Todo = Object.assign({}, todo, part);
    this.list.splice(index, 1, newTodo);
  }
}
</script>

<style scoped lang="scss">
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  > .inner {
    border: 1px solid grey;
    padding: 20px;
  }
}
</style>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
ul,
ol {
  list-style: none;
}
</style>

