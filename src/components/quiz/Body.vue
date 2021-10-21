<template>
  <b-card-body body-class="card-body">
    <b-card-title
      ><h4>{{ questionNumber }}. <span v-html="questionText"></span></h4
    ></b-card-title>
    <b-card-text class="mt-4">
      <div
        v-for="questionOption in questionOptions"
        :key="questionOption.id"
        class="question-options"
        @click="$emit('select-answer', questionOption.value)"
      >
        <b-alert show :variant="questionOption.variant">
          <b-row align-v="center">
            <b-col cols="10">
              <span v-html="questionOption.value"></span>
            </b-col>
            <b-col cols="2">
              <b-icon
                v-if="
                  questionOption.variant !== 'secondary' &&
                    questionOption.variant === 'success'
                "
                scale="2"
                class="float-right"
                icon="check-circle"
                variant="success"
              ></b-icon>

              <b-icon
                v-else-if="
                  questionOption.variant !== 'secondary' &&
                    questionOption.variant === 'danger'
                "
                scale="2"
                class="float-right"
                icon="x-circle"
                variant="danger"
              ></b-icon>
            </b-col>
          </b-row>
        </b-alert>
      </div>
    </b-card-text>
  </b-card-body>
</template>

<script>
export default {
  props: ["question", "questionIndex", "selectedAnswer"],
  emits: ["selectAnswer"],
  computed: {
    questionNumber() {
      return this.questionIndex + 1;
    },
    questionText() {
      return this.question.question;
    },
    questionOptions() {
      const questionOptions = this.question.options.map((option, index) => {
        let variant = "secondary";

        if (this.selectedAnswer && this.question.correct_answer === option) {
          variant = "success";
        } else if (this.selectedAnswer && this.selectedAnswer === option) {
          variant = "danger";
        }

        return {
          id: index,
          value: option,
          variant,
        };
      });

      return questionOptions;
    },
  },
};
</script>

<style scoped>
.card-body {
  padding: 0.4rem 1.25rem;
}
.question-options {
  cursor: pointer;
}
</style>
