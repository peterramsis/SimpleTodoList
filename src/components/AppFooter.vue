<template>
  <footer v-show="isShow">
    this my app
    <router-link to="/about">About</router-link>
  </footer>
</template>
<style scoped>
footer {
  display: flex;
  justify-content: center;
  border: 2px solid #ccc;
  padding: 10px;
  flex-direction: column;
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
