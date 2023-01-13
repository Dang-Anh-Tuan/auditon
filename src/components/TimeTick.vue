<template>
  <div class="container-time-tick">
    <p class="hidden">{{ percentCom }}</p>
    <div ref="circle" class="circle"></div>
    <div class="mark"></div>
  </div>
</template>

<script>
export default {
  props: {
    percent: {
      type: Number,
      default: 0,
    },
  },

  computed: {
    percentCom: {
      get() {
        return this.percent;
      },
    },
  },

  updated() {
    if (this.$refs?.circle) {
      const position = `${((200 - 19) * this.percentCom) / 100}px`;
      this.$refs.circle.style.left = position;
    }
  },
};
</script>

<style scoped>
.container-time-tick {
  position: relative;
  margin-top: 32px;
  margin-right: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 200px;
  background: rgba(0, 0, 0, 0.1);
  height: 20px;
  border-radius: 999999px;
  border: 1px solid #fff;
  box-shadow: 0 0 0.25em 0 #fff;
}

.mark {
  position: absolute;
  top: 0;
  right: 30px;
  width: 60px;
  height: 100%;
  display: flex;
  border-radius: 3px;
  overflow: hidden;
  box-shadow: 0 0 0.5em 0 rgba(156, 252, 248, 1);
  animation: showHide 2.5s linear infinite;
  background-image: linear-gradient(
    to right,
    #9cfcf8,
    #aaf7ff,
    #bef1ff,
    #d1ecff,
    #dfe8f6,
    #dfe8f6,
    #dfe8f6,
    #dfe8f6,
    #d1ecff,
    #bef1ff,
    #aaf7ff,
    #9cfcf8
  );
}

.circle {
  position: absolute;
  top: 2px;
  left: 180px;
  height: 16px;
  width: 16px;
  background: radial-gradient(#fff 10%, #e7432e 70%);
  border-radius: 50%;
  box-shadow: 0 0 2px 3px #fff;
  z-index: 1;
}

.hidden {
  opacity: 0;
}

@keyframes showHide {
  0% {
    opacity: 0.5;
  }
  30% {
    opacity: 1;
  }
  70% {
    opacity: 1;
  }
  100% {
    opacity: 0.5;
  }
}
</style>
