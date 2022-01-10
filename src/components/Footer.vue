<template>
  <div>
    <label for="">
      <input type="checkbox" :checked="isTrue" />
    </label>
    <span
      ><span>已完成{{ count }}</span
      >/全部{{ todos.length }}</span
    >
    <button>清除已完成任务</button>
  </div>
</template>
<script lang="ts">
import { Todo } from "@/assets/type/todo";
import { computed, defineComponent, ref, watch } from "vue";
export default defineComponent({
  name: "Footer",
  props: {
    todos: {
      type: Array as () => Todo[],
      required: true,
    },
  },
  setup(props) {
    const isTrue = ref(false);

    watch(
      isTrue,
      () => {
        console.log(isTrue.value, "isTrue");
      },
      { immediate: true }
    );

    const count = computed(() => {
      return props.todos.reduce(
        (pre, todo, index) => pre + (todo.isCompleted ? 1 : 0),
        0
      );
    });
    return { count };
  },
});
</script>

<style lang="scss" scoped>
</style>