<template>
  <div class="container-character">
    <video class="character" autoplay="autoplay" loop="true">
      <source src="@/assets/video/character.mp4" type="video/mp4" />
    </video>
  </div>
</template>

<script>
export default {
  name: "characterVue",
};
</script>

<style scoped>
.character {
  width: 300px;
}
</style>
