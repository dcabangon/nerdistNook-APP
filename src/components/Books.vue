<template>
  <div>
    <!-- <h1>Books</h1> -->
    <section class="books">
      <div class="row">
        <BookCard
        v-on:delete-book="deleteBook"
        v-on:update-book="update"
        v-for="book in books"
        v-bind:key="book._id"
        :id="book._id"
        :name="book.bookName"
        :publisher="book.publisher"
        :book="book"
        :imageLink="book.imageLink"
      />
      </div>
    </section>
  </div>
</template>

<script>
const BASE_API_URL =
  "https://3000-dcabangon-nerdistnookapi-7e4pnbeivwk.ws-us30.gitpod.io/";

import axios from "axios";
import BookCard from "@/components/BookCard.vue";

export default {
  name: "Books",
  components: { BookCard },

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
      this.$emit("update-book", bookId);
    },

    refreshData: async function () {
      let response = await axios.get(BASE_API_URL + "books");
      this.books = response.data;
    },

    deleteBook: async function (bookId) {
      if (
        confirm(
          "Are you sure you want to delete this entry? Press OK to confirm"
        )
      ) {
        await axios.delete(BASE_API_URL + "books/" + bookId);
        this.refreshData();
        alert("Delete Outfit Successful!");
      }
    },
  },
};
</script>