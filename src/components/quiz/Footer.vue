<template>
  <b-row>
    <b-col md="6" class="text-center text-sm-center text-md-left">
      <div class="question-tracker">
        {{ questionNumber }} of {{ questionsCount }} Questions
      </div>
    </b-col>
    <b-col md="6" class="text-center text-sm-center text-md-right">
      <b-button
        variant="primary"
        :disabled="!selectedAnswer"
        @click="$emit('next')"
        >Next</b-button
      >
    </b-col>
  </b-row>
</template>

<script>
export default {
  props: ["questions", "questionIndex", "selectedAnswer"],
  emits: ["next"],
  computed: {
    questionNumber() {
      return this.questionIndex + 1;
    },
    questionsCount() {
      return this.questions.length;
    },
  },
};
</script>

<style scoped>
.question-tracker {
  padding: 0.375rem 0.75rem;
}
</style>
