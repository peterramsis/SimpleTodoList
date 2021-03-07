<template>
  <div>
    <form :class="{ hiddenForm: toggleForm, add_task: true }">
      <input type="text" v-model="task" placeholder="Task" />
      <input type="text" v-model="text" placeholder="Text" />
      <div class="reminder">
        <input type="checkbox" v-model="reminder" placeholder="reminder" />
        <label for="">Reminder</label>
      </div>
      <input type="submit" value="Add" @click.prevent="addTask" />
    </form>
  </div>
</template>

<style lang="scss" scoped>
.hiddenForm {
  display: none !important;
}
.add_task {
  display: flex;
  flex-direction: column;
  .reminder {
    padding: 10px;
  }
  input[type="text"] {
    padding: 28px;
    margin-bottom: 8px;
  }
  input[type="submit"] {
    padding: 20px;
    background-color: beige;
    border: none;
    margin-bottom: 10px;
  }
}
</style>

<script>
export default {
  name: "add-task",
  props: {
    toggleForm: { type: Boolean, require: true }
  },
  data() {
    return {
      text: "",
      task: "",
      reminder: false
    };
  },
  methods: {
    async addTask() {
      const task = {
        text: this.text,
        task: this.task,
        reminder: this.reminder
      };

      this.$emit("addTask", task);
      this.text = "";
      this.task = "";
      this.reminder = false;
    }
  }
};
</script>
