<template>
  <div class="hoverImage">
    <auto-rotate
      :image="this.image"
      :duration="this.duration"
      :reverse="this.reverse"
    ></auto-rotate>
  </div>
</template>

<script>
import AutoRotate from "./AutoRotate.vue";
export default {
  components: { AutoRotate },
  name: "HoverRotate",
  props: ["image", "duration", "reverse"],
};
</script>

<style>
.hoverImage {
  width: 12vw;
  height: 12vw;
  object-fit: contain;
  animation: scaleBack 0.125s 1 linear;
}
.hoverImage:hover {
  animation: scaleForward 0.125s 1 linear;
  transform: scale(1.1);
}

@keyframes scaleForward {
  from {
    transform: scale(1);
  }
  to {
    transform: scale(1.1);
  }
}
@keyframes scaleBack {
  from {
    transform: scale(1.1);
  }
  to {
    transform: scale(1);
  }
}
</style>