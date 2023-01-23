<template>
  <!-- TODO: implement me -->
  <img src='@/assets/BooksListPagination.jpg' class='img-fluid rounded' alt=''>
  <div class="mt-3 btn-toolbar justify-content-center" role="toolbar">
    <div class="btn-group" role="group">
    <button
      type="button"
      id="pagination-back-button"
      class="btn btn-link btn-outline-secondary"
      :class= "{disabled: firstPage}"
      :disabled= "firstPage"
      @click="updatePage(this.page - 1)"
      >
      Previous
    </button>
    <button
      type="button"
      id="pagination-next-button"
      class="btn btn-link btn-outline-secondary"
      :class= "{disabled: lastPage}"
      :disabled= "lastPage"
      @click="updatePage(this.page + 1)"
      >
      Next
    </button>
  </div>
</div>
</template>

<script>
export default {
  name: 'BooksListPagination',
  props: {
    page: Number,
    windowSize: Number,
    booksLength: Number,
  },
  computed: {
    firstPage() {
      return this.page === 0;
    },
    lastPage() {
      return this.page === Math.ceil(this.booksLength / this.windowSize) - 1;
    },
  },
  methods: {
    updatePage(page) {
      this.$emit('update-page', page);
    },
  },
  emits: ['update-page'],
};
</script>

<style scoped>
button {
  text-decoration: none;
}
</style>