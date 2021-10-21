<template>
  <b-form>
    <b-form-group label="Category:" label-for="category">
      <b-form-select
        id="category"
        v-model="form.category"
        :options="categories"
        @change="categoryChange"
      ></b-form-select>
    </b-form-group>

    <b-form-group label="Difficulty:" label-for="difficulty">
      <b-form-select
        id="difficulty"
        v-model="form.difficulty"
        :options="difficulties"
        @change="difficultyChange"
      ></b-form-select>
    </b-form-group>
  </b-form>
</template>

<script>
export default {
  props: ["settings"],
  emits: ["category-change", "difficulty-change"],
  data() {
    return {
      form: {
        category: "any",
        difficulty: "any",
      },
      categories: [
        { id: 1, value: "any", text: "Any Category" },
        { id: 2, value: "27", text: "Animals" },
        { id: 3, value: "25", text: "Art" },
        { id: 4, value: "26", text: "Celebrities" },
        { id: 5, value: "16", text: "Entertainment: Board Games" },
        { id: 6, value: "10", text: "Entertainment: Books" },
        { id: 7, value: "32", text: "Entertainment: Cartoon &amp; Animations" },
        { id: 8, value: "29", text: "Entertainment: Comics" },
        { id: 9, value: "11", text: "Entertainment: Film" },
        {
          id: 10,
          value: "31",
          text: "Entertainment: Japanese Anime &amp; Manga",
        },
        { id: 11, value: "12", text: "Entertainment: Music" },
        { id: 12, value: "13", text: "Entertainment: Musicals &amp; Theatres" },
        { id: 13, value: "14", text: "Entertainment: Television" },
        { id: 14, value: "15", text: "Entertainment: Video Games" },
        { id: 15, value: "9", text: "General Knowledge" },
        { id: 16, value: "22", text: "Geography" },
        { id: 17, value: "23", text: "History" },
        { id: 18, value: "20", text: "Mythology" },
        { id: 19, value: "24", text: "Politics" },
        { id: 20, value: "18", text: "Science: Computers" },
        { id: 21, value: "30", text: "Science: Gadgets" },
        { id: 22, value: "19", text: "Science: Mathematics" },
        { id: 23, value: "17", text: "Science &amp; Nature" },
        { id: 24, value: "21", text: "Sports" },
        { id: 25, value: "28", text: "Vehicles" },
      ],
      difficulties: [
        { id: 1, value: "any", text: "Any Difficulty" },
        { id: 1, value: "easy", text: "Easy" },
        { id: 1, value: "medium", text: "Medium" },
        { id: 1, value: "hard", text: "Hard" },
      ],
    };
  },
  methods: {
    categoryChange(value) {
      this.$emit("category-change", value);
    },
    difficultyChange(value) {
      this.$emit("difficulty-change", value);
    },
  },
  created() {
    this.form = this.settings;
  },
};
</script>
