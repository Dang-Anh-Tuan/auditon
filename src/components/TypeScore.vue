<template>
  <div
    :class="{
      invisible: !isShowTypeScore,
      visible: isShowTypeScore,
    }"
    class="container-character container-type-core"
  >
    <p
      class="type-score"
      :class="{
        'type-core--perfect': typeScore === 'Perfect',
        'type-core--great': typeScore === 'Great',
        'type-core--cool': typeScore === 'Cool',
        'type-core--miss': typeScore === 'Miss',
      }"
    >
      {{ typeScore }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    isShowTypeScore: Boolean,
    typeScore: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped>
.type-score {
  width: 100%;
  text-align: center;
  margin-bottom: 20px;
  font-size: 4rem;
  font-family: "Pacifico", sans-serif;
  -webkit-text-stroke: 3px white;
}

.container-type-core {
  height: 150px;
}

.type-core--perfect {
  background: -webkit-linear-gradient(#fff, #d23fce);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.type-core--great {
  background: -webkit-linear-gradient(#fff, #58963b);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.type-core--cool {
  background: -webkit-linear-gradient(#fff, #0215bd);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.type-core--miss {
  background: -webkit-linear-gradient(#fff, #e65290);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
