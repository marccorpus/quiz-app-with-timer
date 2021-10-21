<template>
  <b-modal
    id="modal"
    :title="title"
    :no-close-on-backdrop="true"
    ok-only
    :ok-title="buttonCaption"
  >
    <slot></slot>
  </b-modal>
</template>

<script>
export default {
  props: ["title", "buttonCaption"],
};
</script>
