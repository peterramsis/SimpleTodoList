<template>
  <div id="app">
    <AddTask @addTask="fireAddTask" :toggleForm="toggle" />
    <Task :tasks="tasks" @delete-task="deleteTask" @reminderTask="reminder" />
  </div>
</template>

<style lang="scss">
* {
  box-sizing: border-box;
}
#app {
  width: 500px;
  margin: auto;
}
</style>

<script>
import Task from "@/components/Task.vue";
import AddTask from "@/components/addTask.vue";
export default {
  name: "App",
  data() {
    return {
      tasks: []
    };
  },
  props: {
    toggle: {
      require: true,
      type: Boolean
    }
  },
  methods: {
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE"
      });

      res.status == 200
        ? (this.tasks = this.tasks.filter(task => task.id != id))
        : alert("erro");
    },
    async reminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const upreminder = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(upreminder)
      });

      const data = res.json();

      this.tasks = await this.tasks.map(task =>
        task.id === id ? { ...task, reminder: !data.reminder } : task
      );
    },
    async fireAddTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(task)
      });
      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    ToggleForm() {
      this.toggle = !this.toggle;
    },
    async fetchTasks() {
      const res = await fetch(`api/tasks`);
      const data = await res.json();
      console.log(data);
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      console.log(data);
      return data;
    }
  },
  components: {
    Task,
    AddTask
  },
  async created() {
    this.fetchTasks().then(tasks => (this.tasks = tasks));
    console.log(this.tasks);
  }
};
</script>
