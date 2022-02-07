<template>
  <b-row>
    <b-col cols="3"> </b-col>
    <b-col cols="6">
      <b-input-group key="sm" size="sm" class="mb-3">
        <b-form-input v-model="bookName" v-on:keyup.enter="search()" placeholder="Search by Name">
        </b-form-input>
        <b-form-input v-model="publisher" v-on:keyup.enter="search()" placeholder="Search by Publisher">
        </b-form-input>
        <b-input-group-append>
          <b-button
            size="md"
            text="Button"
            variant="warning"
            v-on:click="search()"
            >Search</b-button
          >
        </b-input-group-append>
      </b-input-group>
    </b-col>

    <b-col cols="3"></b-col>
  </b-row>
</template>

<script>
export default {
  data: function () {
    return {
      bookName: "",
      publisher: "",
    };
  },
  methods: {
    search: function () {
      let data = {
        bookName: this.bookName,
        publisher: this.publisher,
      };
      this.$emit("search-book", data);
    },
  },
};
</script>
