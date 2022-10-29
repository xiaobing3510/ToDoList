<template>
  <section class="todoapp">
    <!-- 传入的所有list均为筛选后的数组showArr -->
    <!-- 传入list, 定义接收添加事件函数与全选改变事件-->
    <TodoHeader :list="showArr" @add="addFn" @checked="checkedFn"></TodoHeader>
    <!-- 传入list, 定义接收子事件勾选函数与删除函数 -->
    <TodoMain :list="showArr" @change="changeFn" @del="delFn"></TodoMain>
    <!-- 传入list selected, 定义清除已完成函数 -->
    <TodoFooter
      :list="showArr"
      :selected="selected"
      @clear="clearFn"
      @switch="switchFn"
    ></TodoFooter>
  </section>
</template>

<script>
// 1.0 样式引入
import './styles/base.css'
import './styles/index.css'

import TodoHeader from './components/TodoHeader'
import TodoMain from './components/TodoMain'
import TodoFooter from './components/TodoFooter'

export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      // 打开时从本地获取list数据,没有则为空数组
      list: JSON.parse(localStorage.getItem('ToDoList')) || [],
      // 设置完成状态属性
      selected: 'all',
    }
  },
  methods: {
    // 调用时接收id将对应isDone取反
    changeFn(id) {
      const res = this.list.find((i) => i.id === id)
      res.isDone = !res.isDone
    },
    // 调用时接收id删除对应事件
    delFn(id) {
      this.list = this.list.filter((i) => i.id !== id)
    },
    // 调用时接收name向list添加一个对象
    addFn(name) {
      this.list.push({
        id: this.list.length ? this.list.at(-1).id + 1 : 100,
        name,
        isDone: false,
      })
    },
    // 调用时设置所有的isDone为val
    checkedFn(val) {
      this.list.forEach((i) => (i.isDone = val))
    },
    // 调用时筛选出未完成事件
    clearFn() {
      this.list = this.list.filter((i) => !i.isDone)
    },
    // 调用时selected的值设置为传入的参数
    switchFn(val) {
      this.selected = val
    },
  },
  computed: {
    // 筛选出与选择框对应的的数组
    showArr() {
      if (this.selected === 'yes') return this.list.filter((i) => i.isDone)
      else if (this.selected === 'no') return this.list.filter((i) => !i.isDone)
      else return this.list
    },
  },
  watch: {
    // 深度监听list变化时保存本地
    list: {
      deep: true,
      handler(val) {
        localStorage.setItem('ToDoList', JSON.stringify(val))
      },
    },
  },
}
</script>
