<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <!-- v-for渲染, 当勾选为true时添加completed类名 -->
    <li :class="{ completed: item.isDone }" v-for="item in list" :key="item.id">
      <div class="view">
        <!-- 设置勾选框初始数据, 并且勾选改变时子传父id调用事件改变isDone  -->
        <input
          class="toggle"
          type="checkbox"
          :checked="item.isDone"
          @change="$emit('change', item.id)"
        />
        <label>{{ item.name }}</label>
        <!-- 删除按钮添加点击事件, 点击时子传父id调用删除事件 -->
        <button class="destroy" @click="$emit('del', item.id)"></button>
      </div>
    </li>
  </ul>
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
}
</script>
