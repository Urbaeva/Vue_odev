<template>
  <div>

    <CreateComponent></CreateComponent>
    <IndexComponent/>

  </div>
</template>

<script>
import IndexComponent from "./components/IndexComponent.vue";
import CreateComponent from "./components/CreateComponent.vue";
import router from "@/router";
export default  {
  name: 'App',

  components: {
    IndexComponent,
    CreateComponent,
  },

  router

}
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
