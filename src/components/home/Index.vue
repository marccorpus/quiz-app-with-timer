<template>
  <div>
    <div class="home">
      <b-row class="mb-3">
        <b-col sm="6" offset-sm="3" class="text-center">
          <b-button
            @click="$emit('start-quiz')"
            size="lg"
            class="shadow-none button"
            >Start Quiz</b-button
          >
        </b-col>
      </b-row>

      <SettingsBtn @toggle-modal="toggleModal" />

      <HowToPlayBtn @toggle-modal="toggleModal" />
    </div>

    <Modal :title="modal.title" :button-caption="modal.buttonCaption"
      ><component
        :is="modal.component"
        :settings="settings"
        @category-change="categoryChange"
        @difficulty-change="difficultyChange"
    /></Modal>
  </div>
</template>

<script>
import SettingsBtn from "./settings/SettingsBtn.vue";
import Settings from "./settings/Settings.vue";

import HowToPlayBtn from "./how_to_play/HowToPlayBtn.vue";
import HowToPlay from "./how_to_play/HowToPlay.vue";

import Modal from "../ui/Modal.vue";

export default {
  props: ["settings"],
  emits: ["category-change", "difficulty-change", "start-quiz"],
  data() {
    return {
      modal: {
        title: "",
        component: "",
        buttonCaption: "",
      },
    };
  },
  methods: {
    toggleModal({ visibility, title, component, buttonCaption }) {
      this.modal = {
        title,
        component,
        buttonCaption,
      };

      if (visibility) {
        this.$bvModal.show("modal");
      } else {
        this.$bvModal.hide("modal");
      }
    },
    categoryChange(value) {
      this.$emit("category-change", value);
    },
    difficultyChange(value) {
      this.$emit("difficulty-change", value);
    },
  },
  components: {
    SettingsBtn,
    Settings,
    HowToPlayBtn,
    HowToPlay,
    Modal,
  },
};
</script>

<style scoped>
.home {
  margin-top: 150px;
}
.button,
.button:hover,
.button:focus {
  background-color: #fff !important;
  border: none;
  border-radius: 5px;
  color: #2c62ef !important;
  font-weight: bold;
  padding: 10px 25px;
}
</style>
