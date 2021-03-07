<template>
  <header v-show="isShow">
    <h2>{{ title }}</h2>
    <button @click="$emit('toggle')">
      {{ textShow == true ? "AddTask" : "Close" }}
    </button>
  </header>
</template>

<style lang="scss" scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ccc;
  padding: 10px;
  color: #ccc;
  background-color: #2d3436;
  button {
    padding: 10px;
    border: none;
    background-color: green;
    color: white;
  }
}
</style>

<script>
export default {
  name: "AppHeader",
  props: {
    title: {
      type: String
    },
    textShow: {
      type: Boolean
    }
  },
  computed: {
    isShow() {
      if (this.$route.name == "Home") {
        return true;
      } else {
        return false;
      }
    }
  }
};
</script>
