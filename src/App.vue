<template>
  <register />
  <logIn />
  <todo />
</template>

<script>
import register from "./components/register.vue";
import logIn from "./components/logIn.vue";
import todo from "./components/todo.vue";

export default {
  name: "App",
  components: {
    register,
    logIn,
    todo,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
