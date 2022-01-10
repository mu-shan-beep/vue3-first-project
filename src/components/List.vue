<template>
  <ul>
    <Item
      v-for="item in todos"
      :key="item.id"
      :todo="item"
      :index="index"
      :deleteTodo="deleteTodo"
      :updateTodo="updateTodo"
    />
  </ul>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import Item from "./Item.vue";
export default defineComponent({
  name: "List",
  components: {
    Item,
  },
  props: {
    todos: {},
    deleteTodo: {
      type: Function,
    },
    updateTodo: {},
  },
  setup() {},
});
</script>

<style lang="scss" scoped>
</style>