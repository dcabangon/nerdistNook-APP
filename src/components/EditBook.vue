<template>
  <div class="editbook-div">
    <div class="margin-form">
      <h1>Edit Book</h1>
      <div>
        <label>Book Name</label>
        <input type="text" v-model="bookName" class="form-control" />
      </div>

      <div>
        <label>Issue</label>
        <input type="text" v-model="issueNumber" class="form-control" />
      </div>

      <div>
        <label>Publisher</label>
        <input type="text" v-model="publisher" class="form-control" />
      </div>

      <div>
        <label>Review</label>
        <input type="text" v-model="review" class="form-control" />
      </div>

      <div>
        <label>Image Link</label>
        <input type="text" v-model="imageLink" class="form-control" />
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
      rating: "",
      issueNumber: "",
      review: "",
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
    this.issueNumber = book.issueNumber;
    this.review = book.review;
  },

  props: ["bookId"],

  methods: {
    updateBook: async function () {
      await axios.patch(BASE_API_URL + "books/" + this.bookId, {
        bookName: this.bookName,
        publisher: this.publisher,
        imageLink: this.imageLink,
        rating: this.rating,
        issueNumber: this.issueNumber,
        review: this.review,
      });
      this.$emit("book-updated");
    },
  },
};
</script>

<style scoped>
.editbook-div {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

}

.margin-form {
  /* margin-top: 50px;
  margin-left: 300px;
  margin-right: 300px; */
  background: white;
  padding: 9px;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  width: 100%;
}
</style>