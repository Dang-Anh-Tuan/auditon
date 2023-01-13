<template>
  <div v-show="arrowButtons.length > 0" class="container-arrow-btn">
    <arrow-button
      v-for="(btn, index) in arrowButtons"
      :key="index"
      :direction="btn.direction"
      :is-check="btn.isCheck"
    ></arrow-button>
  </div>
</template>

<script>
import ArrowButton from "./ArrowButton.vue";
export default {
  components: { ArrowButton },

  props: {
    arrowButtons: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style>
.container-arrow-btn {
  margin-top: 32px;
  display: flex;
  justify-content: center;
  width: 500px;
  background: rgba(0, 0, 0, 0.2);
  padding: 12px 40px;
  border-radius: 999999px;
  border: 3px solid #195b9c;
  box-shadow: 0 0 1em 0 #195b9c;
}
</style>
