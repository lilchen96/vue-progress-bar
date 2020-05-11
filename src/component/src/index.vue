<template>
  <div class="line-progress-bar">
    <div
      class="line inner-line"
      :style="{
        height: this.styleOptions.height + 'px',
        borderRadius: this.styleOptions.height / 2 + 'px',
        backgroundColor: this.styleOptions.backgroundColor,
      }"
      @click="progressJump"
    ></div>
    <div
      class="line outer-line"
      :style="{
        height: this.styleOptions.height + 'px',
        marginTop: '-' + this.styleOptions.height + 'px',
        borderRadius: this.styleOptions.height / 2 + 'px',
        backgroundColor: this.styleOptions.progressColor,
        transform: 'translateX(' + (progressPercent - 100) + '%' + ')',
      }"
    ></div>
    <!-- <div
      class="draggle-point"
      :style="{
        transform:
          'translateX(' + (progressPercent / 100) * progressWidth + 'px' + ')',
      }"
    ></div> -->
  </div>
</template>

<script>
export default {
  name: "IllmaticProgressBar",
  props: {
    styleOptions: {
      type: Object,
      default: () => {
        return {
          height: 30,
          borderWidth: 4,
          progressColor: "#87CEFA",
          backgroundColor: "#EDEDED",
        };
      },
    },
    // 进度条加载总量
    duration: {
      type: Number,
      default: 10,
    },
    // 当前量
    progress: {
      type: Number,
      default: 0,
    },
    // 是否自动播放
    autoPlay: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      progressPercent: 0, // 进度条 0%
      speed: 1, // 进度条速度
      interval: {}, // 定时任务
      progressWidth: 0, // 进度条长度
      progressHeight: 0, //进度条高度
      progressIsRun: false,
    };
  },

  mounted() {
    this.progressWidth = document.querySelector(".inner-line").clientWidth;
    if (this.autoPlay) {
      this.run();
    }
  },

  methods: {
    // 进度条启动
    run() {
      if (!this.progressIsRun) {
        this.refresh();
        this.interval = setInterval(this.refresh, 12);
        this.progressIsRun = true;
      }
    },

    // 进度条停止
    stop() {
      clearInterval(this.interval);
      this.progressIsRun = false;
    },

    // 重置进度条
    reset() {
      this.progressPercent = 0;
    },

    // 进度条速度计算
    getSpeed(duration) {
      // 100 份
      const speed = (100 / duration / 1000) * 12;
      return speed;
    },

    // 刷新进度条
    refresh() {
      this.progressPercent += this.speed;
      if (100 - this.progressPercent <= this.speed) {
        this.progressPercent = 100;
        clearInterval(this.interval);
      }
    },

    // 点击进度条 跳进度
    progressJump(e) {
      const positionX = e.offsetX;
      this.progressPercent = (positionX / this.progressWidth) * 100;
      this.$emit("progressJump", this.progressPercent);
    },
  },

  watch: {
    progress: {
      handler() {
        if (this.progress === 0) {
          this.progressPercent = 0;
        } else {
          this.progressPercent = (this.progress / this.duration) * 100;
        }
      },
      immediate: true,
    },
    duration: {
      handler() {
        this.speed = this.getSpeed(this.duration);
      },
      immediate: true,
    },
  },
};
</script>

<style lang="less" scoped>
.line-progress-bar {
  overflow: hidden;
  .line {
    width: 100%;
    border-radius: 10px;
  }
  .inner-line {
  }

  .outer-line {
    pointer-events: none;
  }
  .draggle-point {
    position: absolute;
    background-color: blue;
    width: 8px;
    height: 8px;
    border-radius: 50%;
  }
}
</style>
