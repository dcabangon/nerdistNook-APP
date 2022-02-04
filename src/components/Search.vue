<template>
  <b-row>
    <b-col cols="4"></b-col>
    <b-col cols="4">
      <b-input-group key="sm" size="sm" class="mb-3">
        <b-form-input v-model="bookName" v-on:keyup.enter="search()">
      
        </b-form-input>
        <b-input-group-append>
          <b-button size="md" text="Button" variant="success" v-on:click="search()">Search</b-button>
        </b-input-group-append>
      </b-input-group>
    </b-col>
    <b-col cols="4"></b-col>
  </b-row>
</template>

<script>
export default {
  data: function () {
    return {
      bookName: '',
    };
  },
  methods: {
    search: function () {
      this.$emit("search-book", this.bookName);
    }
  }
}
</script>
