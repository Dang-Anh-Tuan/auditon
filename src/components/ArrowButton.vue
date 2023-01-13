<template>
  <div class="arrow-button" :class="{ 'btn-check': isCheck }">
    <i class="fa-solid fa-arrow-right arrow" :class="getDirectionArrow"></i>
  </div>
</template>

<script>
import constants from "@/constants";

export default {
  props: {
    direction: {
      type: Number,
      default: constants.RIGHT,
    },

    isCheck: Boolean,
  },

  computed: {
    getDirectionArrow() {
      if (this.direction === constants.UP) return "arrow-up";
      if (this.direction === constants.DOWN) return "arrow-down";
      if (this.direction === constants.LEFT) return "arrow-left";
      return "";
    },
  },
};
</script>

<style scoped>
.arrow-button {
  width: 50px;
  height: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  background-image: linear-gradient(
    135.6deg,
    rgba(156, 252, 248, 1) 11.2%,
    rgba(110, 123, 251, 1) 91.1%
  );
  border-radius: 50%;
  margin: 0 4px;
  transition: all 0.5s;
}

.arrow {
  font-size: 2rem;
  color: white;
  height: fit-content;
}

.arrow-up {
  transform: rotate(-90deg);
}

.arrow-down {
  transform: rotate(90deg);
}

.arrow-left {
  transform: rotate(180deg);
}

.btn-check {
  background-image: linear-gradient(135.6deg, #f9d976 11.2%, #f39f86 91.1%);
}
</style>
