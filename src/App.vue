<template>
  <div id="app">
    <AppHeader title="Todolist" @toggle="ToggleForm" :textShow="toggle" />
    <router-view :toggle="toggle"></router-view>
    <AppFooter :textShow="toggle" />
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
import AppHeader from "@/components/AppHeader.vue";
import AppFooter from "@/components/AppFooter.vue";

export default {
  name: "App",
  data() {
    return {
      toggle: true
    };
  },
  methods: {
    ToggleForm() {
      this.toggle = !this.toggle;
    }
  },
  components: {
    AppHeader,
    AppFooter
  },
  async created() {}
};
</script>
