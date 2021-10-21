<template>
  <div class="loading">
    <b-row>
      <b-col sm="6" offset-sm="3" class="text-center">
        <b-spinner variant="light" class="spinner"></b-spinner>
      </b-col>
    </b-row>
  </div>
</template>

<style scoped>
.loading {
  margin-top: 150px;
}
.spinner {
  height: 3rem;
  width: 3rem;
}
</style>
