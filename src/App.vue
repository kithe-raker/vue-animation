<template>
  <div class="root">
    <physics-box></physics-box>
  </div>
</template>

<script>
import PhysicsBox from "./components/PhysicsBox.vue";
export default {
  components: { PhysicsBox },
  name: "App",
};
</script>

<style>
.root {
  height: 100vh;
  width: 100vw;
  background-color: bisque;
}
</style>