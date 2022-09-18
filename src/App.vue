<template>
  <div>
    <TodoInput @add="onAddNewTask"></TodoInput>
    <TodoList :list="tasklist" class="mt-2"></TodoList>
    <TodoButton v-model:active="activeBtnIndex"></TodoButton>
  </div>
</template>

<script>
import TodoList from './components/tdo-list/TodoList.vue'
import TodoInput from './components/todo-input/TodoInput.vue'
import TodoButton from './components/todo-button/TodoButton.vue'

export default {
  name: 'MyApp',
  data() {
    return {
      // 任务列表的数据
      todolist: [
        { id: 1, task: '周一早晨9点开会', done: false },
        { id: 2, task: '周一晚上8点聚餐', done: false },
        { id: 3, task: '准备周三上午的演讲稿', done: true },
      ],
      // 下一个可用的 id
      nextId: 4,
      activeBtnIndex: 0
    }
  },
  methods: {
    onAddNewTask(taskname) {
      this.todolist.unshift({
        id: this.nextId,
        task: taskname,
        done: false
      })
      this.nextId++
    }
  },
  components: {
    TodoList,
    TodoInput,
    TodoButton
  },
  computed: {
    tasklist() {
      switch(this.activeBtnIndex) {
          case 0:
          return this.todolist
        case 1:
          return this.todolist.filter(x => x.done === true)
        case 2:
          return this.todolist.filter(x => x.done !== true)
      }
    }
  }
}
</script>

<style lang="less" scoped>

</style>