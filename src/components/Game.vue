<template>
  <div class="container">
    <img :src="img ||url" />
    <h2>{{ text }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    url: String,
  },
  data() {
    return {
      text: "xxxxx",
      img: null,
    };
  },
  methods: {
    async consumirAPI() {
      const { answer, image } = await fetch("https://yesno.wtf/api").then((r) =>
        r.json()
      );
      console.log(answer);
      console.log(image);
      this.text = answer;
      this.img = image;
    },
  },
};
</script>

<style>
img {
  width: 200px;
  height: 200px;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
