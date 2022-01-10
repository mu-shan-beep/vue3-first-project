<template>
  <Header :addTodo="addTodo" />
  <List :todos="todos" :deleteTodo="deleteTodo" :updateTodo="updateTodo" />
  <Footer :todos="todos" />
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from "vue";
import Header from "@/components/Header.vue";
import List from "@/components/List.vue";
import Footer from "@/components/Footer.vue";

import { Todo } from "@/assets/type/todo";
export default defineComponent({
  components: {
    Header,
    List,
    Footer,
  },
  setup() {
    const list = reactive<{ todos: Todo[] }>({
      todos: [
        {
          id: 1,
          title: "大奔",
          isCompleted: false,
        },
        {
          id: 2,
          title: "宝马",
          isCompleted: true,
        },
        {
          id: 3,
          title: "自行车",
          isCompleted: false,
        },
        {
          id: 4,
          title: "轿车",
          isCompleted: false,
        },
        {
          id: 5,
          title: "三路车",
          isCompleted: true,
        },
      ],
    });

    const addTodo = (todo: Todo) => {
      list.todos.unshift(todo);
    };

    const deleteTodo = (index: number) => {
      list.todos.splice(index, 1);
    };

    const updateTodo = (todo: Todo, isCompeted: boolean) => {
      todo.isCompleted = isCompeted;
    };

    return { ...toRefs(list), addTodo, deleteTodo, updateTodo };
  },
});
</script>
