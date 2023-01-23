<template>
  <!-- TODO: implement me -->
  <img src='@/assets/AuthorSearch.jpg' class='img-fluid rounded' alt=''>
  <label for="author-search">Search books for an author:</label>
  <div class="input-group mb-3">
    <input
      type="text"
      list="authors"
      name="author-search"
      id="author-search"
      class="form-control"
      placeholder="Stephen King, Stephen Hawking, Steve Turner, ..."
      @change="testSearch($event.target.value)"
      />
    <datalist id="authors">
      <option v-for="author in this.authors" :key="author" :value="author"></option>
    </datalist>
  </div>
</template>

<script>
export default {
  name: 'AuthorSearch',
  props: {
    authors: Array,
  },
  methods: {
    testSearch(author){
      if (author !== ""){
        this.$emit('authorSelected', author);
      }
    },
  },
  emits: ['authorSelected'],
};
</script>