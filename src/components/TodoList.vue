<template>
  <div>
    <ol class="todoList">
      <li v-for="(todoItem,index) in list" :key="index">
        <input type="checkbox" :checked="todoItem.status === 'done'" 
          @change="changeStatus(todoItem, $event)"
        >{{todoItem.name}}
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Mixins } from 'vue-property-decorator';
import Todo from '../models/Todo';
@Component({
  props: {
    list: Array,
  },
})
export default class TodoList extends Vue {
  changeStatus(todoItem: Todo, e: Event) {
    let checked = (<HTMLInputElement>e.target).checked;
    this.$emit('updateTodo', todoItem, { status: checked ? 'done' : 'todo' });
  }
}
</script>
