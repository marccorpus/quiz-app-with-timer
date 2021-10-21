<template>
  <b-row class="mb-3">
    <b-col sm="6" offset-sm="3" class="text-center">
      <b-button
        @click="
          $emit('toggle-modal', {
            visibility: true,
            title: 'Settings',
            component: 'Settings',
            buttonCaption: 'Save',
          })
        "
        size="sm"
        variant="link"
        class="shadow-none link"
        >Settings</b-button
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
