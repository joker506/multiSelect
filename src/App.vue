<template>
  <div id="app">
    <multiSelect />
  </div>
</template>

<script>
import multiSelect from "@/components/multiSelect";
export default {
  name: "App",

  components: {
    multiSelect,
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
