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
const BASE_API_URL =
  "https://3000-dcabangon-nerdistnookapi-7e4pnbeivwk.ws-us30.gitpod.io/";
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