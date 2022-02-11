<template>
  <div class="gameBdy">
    <div class="block" v-if="showBlock" @click="stopTimer">
      <span class="clickMe">click me!</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      // console.log(this.reactionTime);
      this.$emit("end", this.reactionTime);
    },
  },
};
</script>

<style>
.block {
  /* only styles */
  background-color: rgb(59, 245, 68);
  color: rgb(63, 62, 62);
  border-radius: 16px;
  max-width: 15%;
  max-height: 15%;
  padding: 50px 50px;
  margin: 40px auto;
  text-align: center;
  font-size: 20px;
  font-weight: 700;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.014),
    6.7px 6.7px 5.3px rgba(0, 0, 0, 0.02),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.025),
    22.3px 22.3px 17.9px rgba(0, 0, 0, 0.03),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.036),
    100px 100px 80px rgba(0, 0, 0, 0.05);
}
clickMe:hover {
  font-size: 30px;
  cursor: default;
}
.gameBdy {
  display: flex;
  justify-content: center;
  flex-direction: column;
  gap: 20px;
}
</style>
