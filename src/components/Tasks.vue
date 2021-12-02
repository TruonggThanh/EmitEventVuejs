<template>
  <div :key="task.id" v-for="task in tasks">
    <Task
      :task="task" @delete-task="$emit('delete-task', task.id)"
    />
    <input ref="abc" v-model="message" placeholder="edit me" @focus="onKeyDown">
  </div>
</template>

<script>
import Task from './Task'
export default {
  name: 'Tasks',
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  emits: ['delete-task'],
  methods: {
    onKeyDown() {
      this.$refs.input.focus()
    }
  }
}
</script>