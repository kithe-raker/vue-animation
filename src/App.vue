<template>
  <div class="root">
    <welcome class="welcomeSection" :onChanged="onWelcomed"></welcome>
    <div class="something">
      <transition name="textAnimate" appear
        ><div v-if="this.isWelcomed" class="text">
          <h5 style="font-size: 4.2vw">🥳text จ้า</h5>
          <p style="font-size: 3.2vw">
            It is a long established fact that a reader will be distracted by
            the readable content of a page when looking at its layout. The point
            of using Lorem Ipsum
          </p>
        </div></transition
      >
    </div>
  </div>
</template>

<script>
import Welcome from "./components/Welcome.vue";
export default {
  name: "App",
  components: { Welcome },
  data() {
    return { isWelcomed: false };
  },
  methods: {
    onWelcomed(isComplete) {
      if (this.isWelcomed != isComplete) this.isWelcomed = isComplete;
    },
  },
};
</script>

<style>
.root {
  background-color: blueviolet;
}
.welcomeSection {
  position: fixed;
}

.something {
  height: 200vh;
  color: #000;
}
.something .text {
  margin-top: 108vh;
  font-size: 8vw;
  background-color: blueviolet;
  color: aliceblue;
}

.textAnimate-enter-from,
.textAnimate-leave-to {
  opacity: 0;
  transform: translateY(12vh);
}

.textAnimate-enter-active,
.textAnimate-leave-active {
  transition: all 0.5s ease;
}
</style>