<template>
  <div class="editbook-div">
    <div class="margin-form">
      
      <b-alert variant="success" v-model="isSuccess" dismissible
        >Successfully added a book</b-alert
      >
      <b-alert variant="error" v-model="isError" dismissible>Error</b-alert>
      <h1>Edit Book</h1>
      <form v-on:submit.prevent="updateBook">
        <div>
          <label>Book Name<span style="color: red">*</span></label>
          <input type="text" v-model="bookName" class="form-control" required />
        </div>
        <div>
          <label>Issue/Volume#<span style="color: red">*</span></label>
          <input
            type="text"
            class="form-control"
            placeholder="..."
            v-model="issueNumber"
            required
          />
        </div>
        <div>
          <label>Book Type<span style="color: red">*</span></label>
          <select class="form-control" v-model="bookType" required>
            <option value="" disabled>Select a type</option>
            <option value="fiction">Fiction</option>
            <option value="non-fiction">Non Fiction</option>
          </select>
        </div>
        <div>
          <label>Publisher<span style="color: red">*</span></label>
          <input
            type="text"
            class="form-control"
            placeholder="..."
            v-model="publisher"
            required
          />
        </div>
        <div>
          <label>Review</label>
          <input
            type="text"
            class="form-control"
            placeholder="..."
            v-model="review"
          />
          <div>
            <label>Image Link</label>
            <input
              type="text"
              class="form-control"
              placeholder="..."
              v-model="imageLink"
            />
          </div>
        </div>

        <div>
          <label for="tags">Genre</label>
          <b-form-tags
            input-id="tags-basic"
            v-model="genre"
            remove-on-delete
          ></b-form-tags>
        </div>

        <div>
          <label>Rating</label>
          <b-form-rating
            v-model="rating"
            variant="warning"
            class="mb-2"
          ></b-form-rating>
        </div>
        <button type="submit" class="my-3 btn btn-warning">Update</button>
      </form>
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
      bookType: "",
      genre: [],
      isSuccess: false,
      isError: false,
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
      var result = await axios.patch(BASE_API_URL + "books/" + this.bookId, {
        bookName: this.bookName,
        publisher: this.publisher,
        imageLink: this.imageLink,
        rating: this.rating,
        issueNumber: this.issueNumber,
        review: this.review,
        bookType: this.bookType,
        genre: this.genre,
      });

      if (result.status == 200) {
        this.isSuccess = true;
      } else this.error = true;
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