
<template>
  <div>
    <div>
      <!-- NAVBAR -->
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand class="header-padding" href="#">NERDISTNOOK</b-navbar-brand>

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
        </b-collapse>
      </b-navbar>
      <!-- END OF NAV BAR -->
      <div class="container">
        <Search class="search-margin" v-if="page != 'add' && page != 'edit'"/>
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
import Search from "@/components/Search";

export default {
  name: "App",
  components: {
    Books,
    AddBook,
    AboutUs,
    EditBook,
    Search,
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

<style scoped>

.search-margin {
margin-top: 20px
}

.header-padding{
  padding-left:10px
}
</style>