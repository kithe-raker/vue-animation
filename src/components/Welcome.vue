<template>
  <div class="section" ref="refSection">
    <hover-rotate
      class="item"
      image="https://cdn.pixabay.com/photo/2017/09/23/16/33/pixel-heart-2779422_1280.png"
      duration="128"
      reverse="true"
    ></hover-rotate>
    <hover-rotate
      class="item2"
      image="https://www.unibetcommunity.com/t5/image/serverpage/image-id/24049i3CDDEE9D860F9723/image-size/large/is-moderation-mode/true?v=1.0&px=999"
      duration="256"
    ></hover-rotate>
    <hover-rotate
      class="item3"
      image="https://cdn.pixabay.com/photo/2017/09/23/16/33/pixel-heart-2779422_1280.png"
      duration="100"
      reverse="true"
    ></hover-rotate>
    <hover-rotate
      class="item4"
      image="https://www.unibetcommunity.com/t5/image/serverpage/image-id/24049i3CDDEE9D860F9723/image-size/large/is-moderation-mode/true?v=1.0&px=999"
      duration="81"
    ></hover-rotate>
    <hover-rotate
      class="item5"
      image="https://cdn.pixabay.com/photo/2017/09/23/16/33/pixel-heart-2779422_1280.png"
      duration="128"
    ></hover-rotate>
    <hover-rotate
      class="item6"
      image="https://www.unibetcommunity.com/t5/image/serverpage/image-id/24049i3CDDEE9D860F9723/image-size/large/is-moderation-mode/true?v=1.0&px=999"
      duration="100"
      reverse="true"
    ></hover-rotate>
    <h1 class="text" ref="centerText">Hello CSS World!</h1>
  </div>
</template>

<script>
import HoverRotate from "./animate/HoverRotate.vue";

export default {
  name: "Welcome",
  components: {
    HoverRotate,
  },
  props: ["onChanged"],
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
    // console.log(this.$refs.refWelcome.style);
  },
  unmounted() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      const scrollY = window.scrollY;

      const scrollOfset = scrollY / this.$refs.refSection.clientHeight;

      this.$refs.refSection.style.opacity = 1 - scrollOfset;
      this.$refs.refSection.style.transform =
        "scale(" + (scrollOfset * 1.6 + 1) + ")";
      this.onChanged(scrollOfset >= 1);
    },
  },
};
</script>

<style>
.section {
  min-height: 100vh;
  width: 100%;
  background-color: blueviolet;
  transform: scale(1);
}

.text {
  position: absolute;
  width: 56vw;
  height: 7.2vw;
  font-size: 7.2vw;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  text-align: center;
  background-color: bisque;
}

.item {
  position: absolute;
  left: 29vw;
  top: 1vh;
}

.item2 {
  position: absolute;
  right: 32vw;
  bottom: 1vh;
}

.item3 {
  position: absolute;
  left: 7vw;
  bottom: 8vh;
}

.item4 {
  position: absolute;
  right: 7vw;
  top: 8vh;
}

.item5 {
  position: absolute;
  right: 7vw;
  bottom: 8vh;
}

.item6 {
  position: absolute;
  left: 7vw;
  top: 12vh;
}
</style>
