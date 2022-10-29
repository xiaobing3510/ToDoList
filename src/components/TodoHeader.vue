<template>
  <header class="header">
    <h1>todos</h1>
    <!-- 动态绑定全选属性 -->
    <input
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
      v-model="checkedAll"
    />
    <label for="toggle-all"></label>
    <!-- 动态绑定输入框的值, 绑定敲击回车事件 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model="count"
      @keyup.enter="add"
    />
  </header>
</template>

<script>
export default {
  props: {
    // 接收list并设置规定数据类型与必须传输
    list: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      // 定义输入框的值
      count: '',
    }
  },
  methods: {
    add() {
      // 先判断输入框是否为空, 不为空再执行
      if (this.count)
        // 当敲击回车时子传父任务名称count以添加任务, 并清空count
        this.$emit('add', this.count)
      this.count = ''
    },
  },
  computed: {
    // 全选属性
    checkedAll: {
      get() {
        // 当数组长度为0时false, 当list全部勾选时为true
        return this.list.length && this.list.every((i) => i.isDone)
      },
      set(val) {
        // 当该属性设置时子传父设置所有的isDone的值val
        this.$emit('checked', val)
      },
    },
  },
}
</script>
