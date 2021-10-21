<template>
  <b-container>
    <Loading v-if="loading" />

    <Home
      v-else-if="!start"
      :settings="settings"
      @category-change="categoryChange"
      @difficulty-change="difficultyChange"
      @start-quiz="startQuiz"
    />

    <Quiz v-else :questions="questions" @end-quiz="endQuiz" />
  </b-container>
</template>

<script>
import axios from "axios";

import Loading from "./Loading.vue";
import Home from "./home/Index.vue";
import Quiz from "./quiz/Index.vue";

export default {
  data() {
    return {
      start: false,

      loading: false,

      questions: [],

      settings: {
        category: "any",
        difficulty: "any",
      },
    };
  },
  methods: {
    categoryChange(value) {
      this.settings.category = value;
    },
    difficultyChange(value) {
      this.settings.difficulty = value;
    },
    generateUrl() {
      let url = "https://opentdb.com/api.php?type=multiple&amount=10";
      if (this.settings.category !== "any") {
        url += `&category=${this.settings.category}`;
      }
      if (this.settings.difficulty !== "any") {
        url += `&difficulty=${this.settings.difficulty}`;
      }

      return url;
    },
    generateQuestions(data) {
      const questions = data.map((question, index) => {
        const options = [
          question.correct_answer,
          ...question.incorrect_answers,
        ];

        const shuffledOptions = options.sort(() => Math.random() - 0.5);

        return {
          id: index,
          category: question.category,
          difficulty: question.difficulty,
          question: question.question,
          options: shuffledOptions,
          correct_answer: question.correct_answer,
        };
      });

      return questions;
    },
    startQuiz() {
      this.loading = true;

      axios.get(this.generateUrl()).then((response) => {
        this.loading = false;

        this.questions = this.generateQuestions(response.data.results);

        if (this.questions.length === 0) {
          this.$bvToast.toast(
            "No data found for your selected category and difficulty. Try to adjust your settings.",
            {
              title: "Oops!",
              variant: "danger",
              autoHideDelay: 5000,
              solid: true,
            }
          );
        } else {
          this.start = true;
        }
      });
    },
    endQuiz() {
      this.start = false;
      this.questions = [];
    },
  },
  components: {
    Loading,
    Home,
    Quiz,
  },
};
</script>
