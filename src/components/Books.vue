<template>
  <div class="main">
    <!-- <h1>Books</h1> -->
    <section class="books">
      <Search
        class="search-margin"
        v-if="page != 'add' && page != 'edit'"
        v-on:search-book="search"
      />
      <b-row>
        <BookCard class="my-3"
          v-on:delete-book="deleteBook"
          v-on:update-book="update"
          v-for="book in books"
          v-bind:key="book._id"
          :id="book._id"
          :name="book.bookName"
          :publisher="book.publisher"
          :book="book"
          :imageLink="book.imageLink"
          :rating="book.rating"
          :writer="book.writer"
          :issueNumber="book.issueNumber"
          :review="book.review"
        />
      </b-row>
    </section>
  </div>
</template>

<script>
import { BASE_API_URL } from "@/env-vars";

import axios from "axios";
import BookCard from "@/components/BookCard.vue";
import Search from "@/components/Search.vue";

export default {
  name: "Books",
  components: { BookCard, Search },

  created: async function () {
    this.getBooks();
  },

  data: function () {
    return {
      books: [],
      page: "Books"
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
    search: async function (bookName) {
      let response = await axios.get(
        BASE_API_URL + "books?bookName=" + bookName
      );
      this.books = response.data;
      //console.log(bookName)
    },
    getBooks: async function () {
      let response = await axios.get(BASE_API_URL + "books");
      this.books = response.data;
    },
  },
};
</script>

<style scoped>
.search-margin {
  margin-top: 20px;
}


</style>