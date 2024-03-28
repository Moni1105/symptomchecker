<template>
<div>
  <h1>Health Information Portal</h1>
  <healthPortal />
</div>
</template>

<script>
//import SymptomCheck from './components/SymptomCheck.vue';
import healthPortal from "./components/healthPortal.vue";
export default {
  name: "App",
  components: {
    healthPortal,
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
