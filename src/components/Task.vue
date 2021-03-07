<template>
  <div class="tasks">
    <div
      v-for="task in tasks"
      :key="task.id"
      :class="{ task: true, reminder: task.reminder }"
      @click="$emit('reminderTask', task.id)"
    >
      <h2>{{ task.task }}</h2>
      <p>{{ task.text }}</p>
      <button class="btn-delete" @click="deleteTask(task.id)">X</button>
    </div>
  </div>
</template>

<style lang="scss" scoded>
.tasks {
  display: flex;
  justify-content: left;
  flex-direction: column;
  .task {
    position: relative;
    background-color: #dfe6e9;
    width: 100%;
    height: 100px;
    margin-bottom: 5px;
    padding: 5px;
    color: #2d3436;
    &.reminder {
      border-left: 4px solid #2d3436;
    }
    .btn-delete {
      color: red;
      position: absolute;
      right: 24px;
      top: 41%;
      border: none;
      background: transparent;
    }
  }
}
</style>

<script>
export default {
  name: "Task",
  props: {
    tasks: {
      required: true
    }
  },
  methods: {
    deleteTask(id) {
      this.$emit("delete-task", id);
    }
  }
};
</script>
