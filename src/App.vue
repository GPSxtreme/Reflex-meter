<template>
  <div class="headCntnr">
    <h1>{{ head }}</h1>
    <button class="btn" @click="start" :disabled="isPlaying">Play</button>
    <p v-if="showResult">
      {{ `Your reaction time is ${this.reactionTime}ms!` }}
    </p>
    <p v-if="showResult">{{ `#${complimentReturner()}` }}</p>
    <p v-if="showResult">Wanna try again? Press on play</p>
  </div>
  <block v-if="isPlaying" :delay="delay" @end="endGame" />
</template>

<script>
//import other vue files
import Block from "./components/Block.vue";
export default {
  data() {
    return {
      head: "Test your reflexes!",
      isPlaying: false,
      delay: null,
      showResult: false,
      reactionTime: null,
    };
  },
  components: { Block },
  methods: {
    start() {
      this.delay = 1000 + Math.random() * 3000;
      this.isPlaying = true;
      this.showResult = false;
    },
    endGame(status) {
      this.isPlaying = false;
      this.showResult = true;
      this.reactionTime = status;
    },
    complimentReturner() {
      if (this.reactionTime <= 180) return "Ninja speed!";
      else if (this.reactionTime <= 280) return "Quick reflexes!";
      else if (this.reactionTime <= 380) return "Meh.. Can be better";
      else if (this.reactionTime <= 580) return "Got any eye problems?";
      else return "Boomer";
    },
  },
};
</script>

<style>
h1 {
  font-size: 20 px;
  text-align: center;
  color: #000;
}
.headCntnr {
  margin-top: 120px;
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-direction: column;
  align-items: center;
}
p {
  text-align: center;
  font-weight: 700;
  font-size: 20px;
}
</style>
