<template>
  <div>
    <h1>Add Book</h1>
    <div>
      <label>Book Name</label>
      <input type="text" v-model="bookName" class="form-control" />
    </div>
    <div>
      <label>publisher</label>
      <input
        type="text"
        class="form-control"
        placeholder="..."
        v-model="publisher"
      />
    </div>
    <div>
      <label>Image Link</label>
      <input
        type="text"
        class="form-control"
        placeholder="..."
        v-model="imageLink"
      />
    </div>
    <button v-on:click="addNew" class="my-3">Add New</button>
  </div>
</template>

<script>
import {BASE_API_URL} from '@/env-vars'
import axios from "axios";
export default {
  data: function () {
    return {
      id: "",
      bookName: "",
      publisher: "",
      imageLink: "",
    };
  },
  methods: {
    addNew: async function () {
      await axios.post(BASE_API_URL + "books", {
        bookName: this.bookName,
        publisher: this.publisher,
        imageLink: this.imageLink,
      });
      this.$emit("new-book-created");
    },
  },
};
</script>