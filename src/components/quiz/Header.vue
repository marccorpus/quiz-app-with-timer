<template>
  <div>
    <b-row align-v="center">
      <b-col cols="10">
        <h5 class="question-category">
          {{ questionCategory }}
        </h5>
        <span class="text-muted">Difficulty: {{ questionDifficulty }}</span>
      </b-col>
      <b-col cols="2">
        <h4 class="float-right">
          <b-badge variant="dark">{{ timeLeft }}</b-badge>
        </h4>
      </b-col>
    </b-row>

    <b-row class="mt-2">
      <b-col>
        <b-progress class="progress-bar" :style="progressBarValue"></b-progress>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  props: ["question", "timeLeft"],
  computed: {
    questionCategory() {
      return this.question.category;
    },
    questionDifficulty() {
      const difficulty = this.question.difficulty;

      return `${difficulty.charAt(0).toUpperCase()}${difficulty.slice(1)}`;
    },
    progressBarValue() {
      const value = ((15 - this.timeLeft) / 15) * 100;

      return {
        width: `${value}%`,
      };
    },
  },
};
</script>

<style scoped>
.question-category {
  margin-top: 4px;
}
.progress-bar {
  height: 3px;
}
</style>
