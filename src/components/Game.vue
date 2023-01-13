<template>
  <div class="container-frame">
    <div class="container-game-play">
      <p class="score">
        <span>{{ score }}</span>
      </p>

      <type-score
        :isShowTypeScore="isShowTypeScore"
        :typeScore="typeScore"
      ></type-score>

      <character></character>

      <time-tick :percent="percent"></time-tick>
      <list-arrow
        :arrow-buttons="arrowBtn"
        :class="{
          invisible: !isShowListBtnArrow,
          visible: isShowListBtnArrow,
        }"
      ></list-arrow>
    </div>
  </div>
</template>

<script>
import ListArrow from "./ListArrow.vue";
import constants from "@/constants";
import TimeTick from "./TimeTick.vue";
import Character from "./Character.vue";
import TypeScore from "./TypeScore.vue";

export default {
  name: "GameAudition",
  components: { ListArrow, TimeTick, Character, TypeScore },

  data() {
    return {
      level: 1,
      arrowBtn: [],
      checkpointType: 0,
      percent: 0,
      isShowListBtnArrow: true,
      removeLoopTimeTick: null,
      score: 0,
      amountPerLevel: 0,
      isShowTypeScore: false,
      typeScore: "",
      removeTimeoutTypeScore: null,
    };
  },

  watch: {
    percent(newVal) {
      if (newVal === 100) {
        this.resetNewTurn();
      }
    },
  },

  created() {
    this.arrowBtn = this.randomListBtn(this.level);

    window.addEventListener("keyup", this.handlePressKey);

    window.addEventListener("click", () => {
      document.querySelector(".character")?.play();
    });

    this.removeLoopTimeTick = setInterval(() => {
      if (this.percent < 100) {
        this.percent++;
      } else {
        this.percent = 0;
      }
    }, constants.SPEED);
  },

  beforeDestroy() {
    if (this.removeLoopTimeTick) {
      clearInterval(this.removeLoopTimeTick);
    }

    window.removeEventListener("keyup", this.handlePressKey);

    window.removeEventListener("click", () => {
      document.querySelector(".character")?.play();
    });
  },

  methods: {
    randomNum() {
      const random = Math.random();
      if (random < 0.25) return 1;
      if (0.25 <= random < 0.5) return 2;
      if (0.5 <= random < 0.75) return 3;
      return 4;
    },

    randomListBtn(level) {
      const arrowButtons = [];
      for (let i = 0; i < level; i++) {
        arrowButtons.push({
          direction: this.randomNum(),
          isCheck: false,
        });
      }

      return arrowButtons;
    },

    getNewListBtn() {
      if (this.level < 7) {
        if (this.amountPerLevel < 3) {
          this.amountPerLevel++;
          this.arrowBtn = this.randomListBtn(this.level);
        } else {
          this.amountPerLevel = 1;
          this.level++;
          this.arrowBtn = this.randomListBtn(this.level);
        }
      } else {
        this.level = 1;
        this.amountPerLevel = 1;
        this.arrowBtn = this.randomListBtn(1);
      }
    },

    randomListBtnByLevel() {
      this.checkpointType = 0;
      this.arrowBtn = this.randomListBtn(this.level);
    },

    handlePressKey(e) {
      let keyCode;
      switch (e.code) {
        case "ArrowUp":
          keyCode = constants.UP;
          break;
        case "ArrowRight":
          keyCode = constants.RIGHT;
          break;
        case "ArrowDown":
          keyCode = constants.DOWN;
          break;
        case "ArrowLeft":
          keyCode = constants.LEFT;
          break;
        case "Space":
          this.handleCheckResult();
          break;
        default:
          break;
      }
      if (this.checkpointType < this.arrowBtn.length) {
        if (this.arrowBtn[this.checkpointType].direction === keyCode) {
          this.arrowBtn[this.checkpointType].isCheck = true;
          this.checkpointType++;
        } else {
          this.checkpointType = 0;
          this.arrowBtn.forEach((item) => (item.isCheck = false));
        }
      }
    },

    resetNewTurn() {
      this.checkpointType = 0;
      this.percent = 0;
      this.getNewListBtn();
      this.isShowListBtnArrow = true;
    },

    handleCheckResult() {
      if (this.isShowListBtnArrow) {
        if (this.removeTimeoutTypeScore) {
          clearTimeout(this.removeTimeoutTypeScore);
        }

        const checkCorrect = this.checkpointType === this.arrowBtn.length;
        if (checkCorrect && 55 <= this.percent && this.percent < 68) {
          this.typeScore = constants.TYPE_SCORES.GREAT;
          console.log(this.typeScore);
          this.score += 2000;
        } else if (checkCorrect && 68 <= this.percent && this.percent <= 72) {
          this.typeScore = constants.TYPE_SCORES.PERFECT;
          this.score += 5000;
        } else if (checkCorrect && 72 < this.percent && this.percent <= 85) {
          this.typeScore = constants.TYPE_SCORES.COOL;
          this.score += 1000;
        } else {
          this.typeScore = constants.TYPE_SCORES.MISS;
        }

        this.isShowTypeScore = true;

        this.removeTimeoutTypeScore = setTimeout(() => {
          this.isShowTypeScore = false;
        }, 1000);

        this.isShowListBtnArrow = false;
      }
    },
  },
};
</script>

<style scoped>
.container-frame {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  background: inherit;
}
.container-game-play {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.score {
  position: absolute;
  top: 10vh;
  right: 30vw;
  font-size: 2.5rem;
  color: white;
  font-family: "Pacifico", sans-serif;
  background: -webkit-linear-gradient(#ec9f05, #ff4e00);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  -webkit-text-stroke: 2px white;
}
</style>
