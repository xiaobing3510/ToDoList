<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong> {{ list.length }}</strong>
    </span>
    <ul class="filters">
      <!-- 给a标签设置class为动态属性, 点击时子传父对应参数调用父级函数改变selected值 -->
      <li>
        <a
          :class="{ selected: selected === 'all' }"
          @click="$emit('switch', 'all')"
          href="javascript:;"
        >
          全部
        </a>
      </li>
      <li>
        <a
          :class="{ selected: selected === 'no' }"
          @click="$emit('switch', 'no')"
          href="javascript:;"
        >
          未完成
        </a>
      </li>
      <li>
        <a
          :class="{ selected: selected === 'yes' }"
          @click="$emit('switch', 'yes')"
          href="javascript:;"
        >
          已完成
        </a>
      </li>
    </ul>
    <!-- v-show设置当页面存在已完成事件时为true, 点击时调用clear函数 -->
    <button
      class="clear-completed"
      v-show="list.some((i) => i.isDone)"
      @click="$emit('clear')"
    >
      清除已完成
    </button>
  </footer>
</template>

<script>
export default {
  props: {
    // 接收list selected并设置规定数据类型与必须传输
    list: {
      type: Array,
      required: true,
    },
    selected: {
      type: String,
      required: true,
    },
  },
}
</script>
