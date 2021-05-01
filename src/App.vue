<template>
  <div id="app">
      <h1>Tarefas brDoctor</h1>
      <TaskProgress :progress="progress"/>
      <NewTask @taskAdded="addTask" />
      <TaskGrid :tasks="tasks" 
                @taskDeleted="deleteTask"
                @taskStateChanged="toggleTaskState"
      />
  </div>
</template>

<script>
import TaskProgress from '@/components/TaskProgress.vue'
import TaskGrid from '@/components/TaskGrid.vue'
import NewTask from  '@/components/NewTask.vue'

export default {
  name: 'app',
  components: {
    TaskGrid, NewTask, TaskProgress
  },
  computed : {
    progress()  {
      const total = this.tasks.length;
      const done = this.tasks.filter(t => t.status==3).length;
      return Math.round(done/total * 100) || 0;
    }
  },
  data() {
    return {
      tasks : []
    }
  },
  watch: {
    // tasks() {
    //   localStorage.setItem('tasks', JSON.stringify(this.tasks));
    // }
    tasks : {
      deep : true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  },
  methods: {
    addTask(task) {
      const reallyNew = this.tasks.filter(t => t.name === task.name).length == 0
      if (reallyNew) {
        this.tasks.push({
          name : task.name,
          status : 1
        })
      }
    },
    deleteTask(task) {
      const indice = this.tasks.indexOf(task);
      this.tasks.splice(indice, 1);
    },
    toggleTaskState(task) {
      const indice = this.tasks.indexOf(task);
      this.tasks[indice].status++;

      if (this.tasks[indice].status>3) {
        this.tasks[indice].status = 1;
      }
    }
  },
  created() {
    const json = localStorage.getItem('tasks');
    const array = JSON.parse(json);

    if (Array.isArray(array)) {
      this.tasks = array
    } else {
      this.tasks = []
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
