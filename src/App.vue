<template>
  <div class="main">
    <div class="top">
      <div v-if="!changeRename">
          <h1 @click="changeRename = true">{{ rename }}</h1>
      </div>
      <div v-if="changeRename">
        <input v-model="rename" placeholder="новое название" @keyup.enter="changeRename = false">
      </div>
    </div>
    <task-form @create="createTask"/>
    <task-list :tasks="tasks" @remove="removeTask" @changedDone="changeDone"/>
  </div>
</template>

<script>
import TaskForm from '@/components/TaskForm.vue'
import TaskList from '@/components/TaskList.vue'

export default {

  components: {
    TaskForm, TaskList
  },

  data () {
    return {
      rename: 'paper',
      changeRename: false,
      tasks: [
        { id: 1, body: 'задача 1', done: false }
      ]
    }
  },

  mounted () {
    this.checkRename()
    this.checkTasks()
  },

  methods: {
    parseStorage () {
      const parsed = JSON.stringify(this.tasks)
      localStorage.setItem('tasks', parsed)
    },
    createTask (task) {
      this.tasks.push(task)
      this.parseStorage()
    },
    removeTask (task) {
      this.tasks = this.tasks.filter(p => p.id !== task.id)
      this.parseStorage()
    },
    changeDone (task) {
      task.done = !task.done
      this.parseStorage()
    },
    checkRename () {
      if (localStorage.rename) {
        this.rename = localStorage.rename
      }
    },
    checkTasks () {
      if (localStorage.getItem('tasks')) {
        try {
          this.tasks = JSON.parse(localStorage.getItem('tasks'))
        } catch (e) {
          localStorage.removeItem('tasks')
        }
      }
    }
  },

  watch: {
    rename (newName) {
      document.title = newName
      localStorage.rename = newName
    }
  }
}

</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
.main {
  text-align: center;
}
.top {
  margin: 15px 0px;
}
</style>
