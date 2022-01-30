<template>
  <div>
    <h1>Books</h1>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Book Name</th>
          <th>Publisher</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="b in books" v-bind:key="b._id">
          <td>{{ b._id }}</td>
          <td>{{ b.bookName }}</td>
          <td>{{ b.publisher }}</td>
          <td>
            <button v-on:click="update(b._id)" class="btn btn-primary btn-sm">
              Edit
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
const BASE_API_URL =
  "https://3000-dcabangon-nerdistnookapi-7e4pnbeivwk.ws-us29.gitpod.io/";
import axios from "axios";
export default {
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
  },


  deleteBook: async function (bookId) {
    if (
      confirm(
        "Are you sure you want to delete this outfit? Press OK to confirm"
      )
    ) {
      // call delete api
      await axios.deleteBook(BASE_API_URL + "books/" + bookId);
      // refresh data list
      this.refreshData();
      alert("Delete Outfit Successful!");
    }
  },
};
</script>