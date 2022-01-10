<template>
  <div>
    <input
      v-model="value"
      @keyup.enter="add"
      type="text"
      placeholder="请输入你的任务名称，请按回车键确认"
    />
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "Header",
  props: {
    addTodo: {
      type: Function,
      required: true, //必须
    },
  },
  setup(props) {
    const value = ref("");

    const add = () => {
      debugger;
      const text = value.value;
      console.log(text.trim(),"text.trim()")
      if (!text.trim()) return;
      const todo = {
        id: Date.now(),
        title: text,
        isCompleted: false,
      };
      props.addTodo(todo);

      value.value = "";
    };
    return {
      value,
      add,
    };
  },
});
</script>

<style lang="scss" scoped>
</style>