<template>
  <div class="addbook-div">
    <div class="addbook-form">
      <h1>Add Book</h1>
      <form v-on:submit="addNew">
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
          <b-form-tags input-id="tags-basic" v-model="genre" remove-on-delete></b-form-tags>
        </div>

        <div>
          <label>Rating</label>
          <b-form-rating
            v-model="rating"
            variant="warning"
            class="mb-2"
          ></b-form-rating>
        </div>
        <button type="submit" class="my-3 btn btn-warning">Add New</button>
      </form>
    </div>
  </div>
</template>

<script>
import { BASE_API_URL } from "@/env-vars";
import axios from "axios";

export default {
  data: function () {
    return {
      id: "",
      bookName: "",
      publisher: "",
      issueNumber: "",
      imageLink: "",
      review: "",
      rating: "",
      bookType: "",
      genre:[],
    };
  },
  methods: {
    addNew: async function () {
      await axios.post(BASE_API_URL + "books", {
        bookName: this.bookName,
        publisher: this.publisher,
        imageLink: this.imageLink,
        issueNumber: this.issueNumber,
        review: this.review,
        rating: this.rating,
        bookType: this.bookType,
        genre: this.genre,
      });
      this.$emit("new-book-created");
    },
  },
};
</script>

<style>
.addbook-div {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.addbook-form {
  background: white;
  padding: 9px;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  width: 100%;
  top: -10%;
}
</style>