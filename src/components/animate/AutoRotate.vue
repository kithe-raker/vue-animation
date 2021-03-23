<template>
  <img class="rotate" ref="rotateRef" :src="this.image" />
</template>

<script>
export default {
  name: "AutoRotate",
  props: ["image", "duration", "reverse"],
  created() {
    const animation = this.reverse ?? false ? "reverseRotation " : "rotation ";
    setTimeout(() => {
      this.$refs.rotateRef.style.animation =
        animation + (this.duration ?? 128) + "s infinite linear";
    }, 200);
  },
};
</script>

<style>
.rotate {
  width: 12vw;
  height: 12vw;
  object-fit: contain;
  /* animation: rotation 128s infinite linear; */
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}

@keyframes reverseRotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(-359deg);
  }
}
</style>