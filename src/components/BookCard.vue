<template>
  <b-col cols="4" class="margin-card">
    <b-card no-body class="overflow-hidden" style="max-width: 540px">
      <b-row no-gutters>
        <b-col>
          <b-card-img
            :src="imageLink"
            alt="Image"
            class="rounded-0"
          ></b-card-img>
        </b-col>
        <b-col>
          <b-card-body :title="name">
            <b-card-text style="max-height: 120px; text-overflow: ellipsis; overflow: hidden;">
              This is a wider card with supporting text as a natural lead-in to
              additional content. This content is a little bit longer.
            </b-card-text>
            <div>
              <b-form-rating
                v-model="rating"
                variant="warning"
                class="mb-2 border-rating" 
                readonly
              ></b-form-rating>
            </div>
            <button
              v-on:click="update(book._id)"
              class="btn btn-primary btn-sm mx-1"
            >
              Edit
            </button>
            <button
              v-on:click="deleteBook(book._id)"
              class="btn btn-danger btn-sm mx-1"
            >
              Delete
            </button>
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </b-col>
</template>

 <script>
import { BASE_API_URL } from "@/env-vars";

import axios from "axios";

export default {
  name: "BookCard",
  props: ["book", "name", "imageLink", "bookID", 'rating'],

  created: async function () {
    let response = await axios.get(BASE_API_URL + "books");
    this.books = response.data;
  },

  data: function () {
    return {
      books: [],
    };
  },

  methods: {
    update: function (bookId) {
      console.log("BookCard Update");
      this.$emit("update-book", bookId);
    },

    refreshData: async function () {
      let response = await axios.get(BASE_API_URL + "books");
      this.books = response.data;
    },

    deleteBook: function (bookId) {
      console.log("BookCard Delete");
      this.$emit("delete-book", bookId);
    },
  },
};
</script>

<style scoped>

.border-rating{
  border: none;
}
.margin-card{
  margin-top: 10px;
}
</style> 