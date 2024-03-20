<template>
  <div>
    <h3>Список задач</h3>
    <task-item class="post" v-for="task in tasks" :key="task.id"
    :task="task"
    @remove="$emit('remove', task)"
    @changedDone="$emit('changedDone', task)"
    />
  </div>
</template>

<script>
import TaskItem from '@/components/TaskItem.vue'

export default {

  components: {
    TaskItem
  },

  props: {
    tasks: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
h3 {
  margin-top: 15px;
}
</style>
