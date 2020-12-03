<template>
  <div class="test">
    <div>watch: count+num：{{ countAddNum }}</div>
    <button @click="addCount">点击+1</button>
  </div>
</template>

<script>
import { ref, computed, watch } from "vue";
export default {
  /* watch方法接收两个参数，第一个参数是一个函数，第二个参数也是个函数，第一个参数函数返回值表示要监听哪个数据，第二个参数函数，表示监听成功后的逻辑，该函数的第一个参数就是监听到目标数据变化后的值。同时watch可以监听多个数据。 */
  name: "Test",
  setup() {
    const count = ref(0); // 定义响应式数据count
    const num = ref(1); // 定义响应式数据num

    const countAddNum = computed(() => {
      // 计算属性
      return count.value + num.value;
    });
    // 相当于watch
    watch(
      [() => count.value, () => num.value],
      ([count, num], [oldCount, oldNum]) => {
        // watch 同时观察count和num两个值
        console.log(
          `count:${count},num:${num} oldCount:${oldCount},oldNum:${oldNum}`
        );
      }
    );
    watch(
      () => {
        return count.value;
      },
      (newcount) => {
        console.log("count变啦", newcount);
      }
    );
    // 相当于methods
    const addCount = () => {
      // 定义增加count方法
      count.value++;
    };

    // 统一return出去
    return {
      count,
      num,
      addCount,
      countAddNum,
    };
  },
};
</script>