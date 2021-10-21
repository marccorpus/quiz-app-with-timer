<template>
  <div class="quiz">
    <b-row>
      <b-col md="10" offset-md="1">
        <b-card>
          <template #header header-class="card-header">
            <Header :question="question" :time-left="timeLeft" />
          </template>

          <Body
            :question="question"
            :question-index="questionIndex"
            :selected-answer="selectedAnswer"
            @select-answer="selectAnswer"
          />

          <template #footer>
            <Footer
              :questions="questions"
              :question-index="questionIndex"
              :selected-answer="selectedAnswer"
              @next="next"
            />
          </template>
        </b-card>
      </b-col>
    </b-row>

    <Modal title="Result" button-caption="Ok">
      <Result :score="score" :questions="questions" />
    </Modal>
  </div>
</template>

<script>
import Modal from "../ui/Modal.vue";
import Result from "./Result.vue";

import Header from "./Header.vue";
import Body from "./Body.vue";
import Footer from "./Footer.vue";

export default {
  props: ["questions"],
  emits: ["end-quiz"],
  data() {
    return {
      questionIndex: 0,

      selectedAnswer: null,

      score: 0,

      timer: null,
      timeLeft: 15,
    };
  },
  computed: {
    question() {
      return this.questions[this.questionIndex];
    },
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.timeLeft -= 1;
      }, 1000);
    },
    resetTimer() {
      clearInterval(this.timer);
    },
    selectAnswer(answer) {
      if (!this.selectedAnswer) {
        this.selectedAnswer = answer;
      }
    },
    next() {
      if (this.questions.length > this.questionIndex + 1) {
        this.questionIndex += 1;
        this.selectedAnswer = null;

        this.timeLeft = 15;
        this.startTimer();
      } else {
        this.$bvModal.show("modal");
      }
    },
  },
  watch: {
    selectedAnswer(value) {
      if (value === this.question.correct_answer) {
        this.score += 1;
      }

      if (value) {
        this.resetTimer();
      }
    },
    timeLeft(value) {
      if (value === 0) {
        this.selectAnswer(new Date().toISOString());
      }
    },
  },
  created() {
    this.startTimer();
  },
  mounted() {
    this.$root.$on("bv::modal::hidden", () => {
      this.$emit("end-quiz");
    });
  },
  components: {
    Modal,
    Result,
    Header,
    Body,
    Footer,
  },
};
</script>

<style scoped>
.quiz {
  margin-top: 40px;
}
.card-header {
  padding-bottom: 0;
}
</style>
