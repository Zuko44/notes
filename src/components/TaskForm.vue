<template>
    <form @submit.prevent>
      <h4>Создание задачи</h4>
      <input
      v-model="task.body"
      class="input"
      type="text"
      placeholder="текст задачи"
      >
      <task-button @click="createTask" class="main_button">
        Создать
      </task-button>
    </form>
</template>

<script>
import TaskButton from '@/components/UI/TaskButton.vue'

export default {

  components: {
    TaskButton
  },

  data () {
    return {
      task: {
        body: '',
        done: false
      }
    }
  },

  methods: {
    createTask () {
      this.task.id = Date.now()
      this.$emit('create', this.task)
      this.task = {
        body: '',
        done: false
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.input {
  width: 95%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
.main_button {
  margin-top: 15px;
}
</style>
