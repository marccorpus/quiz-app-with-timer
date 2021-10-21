<template>
  <b-row class="mt-3">
    <b-col class="text-center">
      <b-icon icon="trophy-fill" variant="primary" class="icon"></b-icon>
      <h5 class="mt-3">You've completed the Quiz!</h5>
      <h5>{{ remarks }}</h5>
    </b-col>
  </b-row>
</template>

<script>
export default {
  props: ["score", "questions"],
  computed: {
    questionsCount() {
      return this.questions.length;
    },
    remarks() {
      let remarks = "";
      const percentage = (this.score / this.questionsCount) * 100;

      if (percentage >= 80) {
        remarks = `Superb 🎉, you got ${this.score} out of ${this.questionsCount}.`;
      } else if (percentage >= 50) {
        remarks = `Cool 😎, you got ${this.score} out of ${this.questionsCount}.`;
      } else {
        remarks = `Sorry 😐, you only got ${this.score} out of ${this.questionsCount}.`;
      }

      return remarks;
    },
  },
};
</script>

<style scoped>
.icon {
  width: 100px;
  height: 100px;
}
</style>
