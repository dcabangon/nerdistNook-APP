
<template>
  <div>
   <div class="container-fluid">
     <!-- navbar -->
     <ul class="nav nav-tabs">
       <li class="nav-item">
         <button v-on:click="goBooks" class="nav-link active" aria-current="page">Books</button>
       </li>
       <li class="nav-item">
         <button v-on:click="goAddBook" class="nav-link">Add New</button>
       </li>
        <li class="nav-item">
         <button v-on:click="goAboutUs" class="nav-link">About Us</button>
       </li>
     </ul>
     <!-- end navbar -->
     
     <div>
       <Books v-if="page==='books'" v-on:update-book="editBook"/>
       <AddBook v-if="page==='add'" v-on:new-book-created="onNewBookCreated"/>
       <AboutUs v-if="page==='about-us'"/>
       <EditBook v-if="page==='edit'" v-bind:bookId="bookBeingEdited" v-on:book-updated="onBookUpdated"/>
       
     </div>
   </div>
 </div>
</template>

<script>
import AddBook from "@/components/AddBook"
import Books from "@/components/Books"
import AboutUs from "@/components/AboutUs"
import EditBook from "@/components/EditBook"

export default {
  name: 'App',
  components: {
     Books, AddBook, AboutUs, EditBook
  },
  data: function() {
    return {
      'page': 'books',
      'bookBeingEdited': 0
    }
  },
  methods:{
    'goBooks': function() {
      this.page = "books"
    },
    'goAddBook': function() {
      this.page = "add"
    },
    'goAboutUs': function() {
      this.page= "about-us"
    },
    'onNewBookCreated':function() {
      this.page="books"
    },
    'editBook': function(bookId) {
      this.page="edit";
      this.bookBeingEdited = bookId;
    },
    'onBookUpdated':function() {
      this.page="books"
    }
  }
}
</script>

<style>
</style>