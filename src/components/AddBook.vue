<template>
  <div class="addbook-div">
    <div class="addbook-form">
      <h1>Add Book</h1>
      <div>
        <label>Book Name</label>
        <input type="text" v-model="bookName" class="form-control" />
      </div>
      <div>
        <label>Issue/Volume#</label>
        <input
          type="text"
          class="form-control"
          placeholder="..."
          v-model="issueNumber"
        />
      </div>
      <div>
        <label>Publisher</label>
        <input
          type="text"
          class="form-control"
          placeholder="..."
          v-model="publisher"
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
        <label>Rating</label>
        <b-form-rating
          v-model="rating"
          variant="warning"
          class="mb-2"
        ></b-form-rating>
      </div>
      <button v-on:click="addNew" class="my-3 btn btn-warning">Add New</button>
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
  top: -10%

}
</style>