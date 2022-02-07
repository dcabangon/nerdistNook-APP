
<template>
  <div class="main">
    <div>
      <!-- NAVBAR -->
      <b-navbar toggleable="lg" type="dark" style="background: red">
        <b-navbar-brand class="header-padding" href="#"
          >NERDISTNOOK</b-navbar-brand
        >

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
      <b-container>
        <Books
          v-if="page === 'books'"
          v-on:update-book="editBook"
          ref="bookComponent"
        />
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
      </b-container>
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
      setTimeout(function () {
         this.$refs.bookComponent.getBooks();
      }, 500);
     
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
.header-padding {
  padding-left: 10px;
}

.main {
  background-image: url("./assets/background.png");
}
</style>