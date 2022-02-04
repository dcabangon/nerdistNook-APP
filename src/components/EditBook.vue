<template>
  <div class="margin-form">
    <h1>Edit Book</h1>
    <div>
      <label>Book Name</label>
      <input type="text" v-model="bookName" class="form-control" />
    </div>
    <div>
      <label>Publisher</label>
      <input type="text" class="form-control" v-model="publisher" />
    </div>
    <div>
      <label>Image Link</label>
      <input type="text" class="form-control" v-model="imageLink" />
    </div>
    <div>
      <label>Rating</label>
      <b-form-rating
        v-model="rating"
        variant="warning"
        class="mb-2"
      ></b-form-rating>
    </div>

    <button v-on:click="updateBook" class="my-3">Update</button>
  </div>
</template>

<script>
// BE SURE TO CHANGE THE API TO THE HEROKU VERSION WHEN YOU DEPLOYED YOUR VUE PROJECT
import { BASE_API_URL } from "@/env-vars";
import axios from "axios";
export default {
  data: function () {
    return {
      id: "",
      bookName: "",
      publisher: "",
      imageLink: "",
      rating:""
    };
  },
  created: async function () {
    let response = await axios.get(BASE_API_URL + "books/" + this.bookId);
    let book = response.data.book;
    this.bookName = book.bookName;
    this.publisher = book.publisher;
    this.id = book.id;
    this.imageLink = book.imageLink;
    this.rating = book.rating;
  },

  props: ["bookId"],

  methods: {
    updateBook: async function () {
      await axios.patch(BASE_API_URL + "books/" + this.bookId, {
        bookName: this.bookName,
        publisher: this.publisher,
        imageLink: this.imageLink,
        rating: this.rating,
      });
      this.$emit("book-updated");
    },
  },
};
</script>

<style scoped>

.margin-form{
  margin-top: 50px;
  margin-left: 300px;
  margin-right: 300px;
}

</style>