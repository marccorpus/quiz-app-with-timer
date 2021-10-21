<template>
  <b-row>
    <b-col sm="6" offset-sm="3" class="text-center">
      <b-button
        @click="
          $emit('toggle-modal', {
            visibility: true,
            title: 'How to Play?',
            component: 'HowToPlay',
            buttonCaption: 'Ok',
          })
        "
        size="sm"
        variant="link"
        class="shadow-none link"
        >How to Play?</b-button
      >
    </b-col>
  </b-row>
</template>

<script>
export default {
  emits: ["toggle-modal"],
};
</script>

<style scoped>
.link {
  color: #fff;
}
.link:focus,
.link:hover {
  color: #fff;
  text-decoration: none;
}
</style>
