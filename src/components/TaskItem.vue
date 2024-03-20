<template>
  <div class="task">
    <div>
      <div>{{ task.body }}</div>
    </div>
    <div class="subtask">
      <div>
        <div>
          <input type="checkbox" :checked="task.done" @click="changedDone">
          <label for="checkbox">done</label>
        </div>
      </div>
      <div class="task_btns">
        <task-button
        @click="$emit('remove', task)"
        >Удалить</task-button>
      </div>
    </div>
  </div>
</template>

<script>
import TaskButton from '@/components/UI/TaskButton.vue'

export default {

  components: {
    TaskButton
  },

  methods: {
    changedDone () {
      this.$emit('changedDone', this.task)
    }
  },

  props: {
    task: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.task {
  padding: 15px;
  border: 2px solid blueviolet;
  text-align: left;
  width: 95%;
  margin: 15px auto 0px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.subtask {
  margin-left: 10px;
  display: flex;
  flex-direction: row;
}
</style>
