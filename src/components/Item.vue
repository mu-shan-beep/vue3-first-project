<template>
  <li
    @mouseenter="mouseHandler(true)"
    @mouseleave="mouseHandler(false)"
    :style="{ backgroundColor: bgColor, color: myColor }"
  >
    <label for="">
      <input type="checkbox" v-model="isComplete" />
      <span>{{ todo.title }}</span>
    </label>
    <button :style="{ display: isShow }" @click="delTodo">删除</button>
  </li>
</template>
<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import { Todo } from "@/assets/type/todo";
export default defineComponent({
  name: "Item",
  props: {
    todo: {
      type: Object as () => Todo, //返回的是Todo类型,
      required: true,
    },
    deleteTodo: {
      type: Function,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
    updateTodo: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const myColor = ref("black");
    const bgColor = ref("white");
    const isShow = ref("none");
    const mouseHandler = (flag: boolean) => {
      if (flag) {
        myColor.value = "yellow";
        bgColor.value = "red";
        isShow.value = "block";
      } else {
        myColor.value = "black";
        bgColor.value = "white";
        isShow.value = "none";
      }
    };

    const delTodo = () => {
      props.deleteTodo(props.index);
    };

    const isComplete = computed({
      get() {
        return props.todo.isCompleted;
      },
      set(val) {
        props.updateTodo(props.todo, val);
      },
    });

    return {
      mouseHandler,
      bgColor,
      myColor,
      isShow,
      delTodo,
      isComplete,
    };
  },
});
</script>

<style lang="scss" scoped>
</style>