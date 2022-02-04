
<template>
  <div>
    <div>
      <!-- NAVBAR -->
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">NERDISTNOOK</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item
              v-on:click="goBooks"
              class="nav-link active"
              aria-current="page"
              >Books</b-nav-item
            >
            <b-nav-item v-on:click="goAddBook" class="nav-link"
              >Add New</b-nav-item
            >
            <b-nav-item v-on:click="goAboutUs" class="nav-link"
              >About</b-nav-item
            >
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-form>
              <b-form-input
                size="sm"
                class="mr-sm-2"
                placeholder="Search"
              ></b-form-input>
              <b-button size="sm" class="my-2 my-sm-0" type="submit"
                >Search</b-button
              >
            </b-nav-form>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
      <!-- END OF NAV BAR -->

      <div>
        <Books v-if="page === 'books'" v-on:update-book="editBook" />
        <AddBook
          v-if="page === 'add'"
          v-on:new-book-created="onNewBookCreated"
        />
        <AboutUs v-if="page === 'about-us'" />
        <EditBook
          v-if="page === 'edit'"
          v-bind:bookId="bookBeingEdited"
          v-on:book-updated="onBookUpdated"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddBook from "@/components/AddBook";
import Books from "@/components/Books";
import AboutUs from "@/components/AboutUs";
import EditBook from "@/components/EditBook";

export default {
  name: "App",
  components: {
    Books,
    AddBook,
    AboutUs,
    EditBook,
  },
  data: function () {
    return {
      page: "books",
      bookBeingEdited: 0,
    };
  },
  methods: {
    goBooks: function () {
      this.page = "books";
    },
    goAddBook: function () {
      this.page = "add";
    },
    goAboutUs: function () {
      this.page = "about-us";
    },
    onNewBookCreated: function () {
      this.page = "books";
    },
    editBook: function (bookId) {
      this.page = "edit";
      this.bookBeingEdited = bookId;
    },
    onBookUpdated: function () {
      this.page = "books";
    },
  },
};
</script>

<style>
</style>