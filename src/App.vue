<template>
  <div class="container-fluid">
    <!-- NAVBAR -->
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <button
          v-on:click="goRecipes"
          class="nav-link active"
          aria-current="page"
        >
          Recipes
        </button>
      </li>
      <li class="nav-item">
        <button v-on:click="goAddRecipe" class="nav-link">Add new</button>
      </li>
    </ul>
    <!-- END OF NAVBAR -->
    <div>
      <Recipes v-if="page === 'recipes'" v-on:update-entry="editEntry" />
      
      <AddRecipe
        v-if="page === 'add'"
        v-on:new-entry-created="onNewEntryCreated"/>
      
      <EditEntry
        v-if="page === 'edit'"
        v-bind:entryId="entryBeingEdited"/>
    </div>
  </div>
</template>   

<script>
import AddRecipe from "@/components/AddRecipe";
import Recipes from "@/components/Recipes";
import EditEntry from "@/components/EditEntry";

export default {
  name: "App",
  components: {
    Recipes,
    AddRecipe,
    EditEntry
  },
 
  data: function () {
    return {
      'page':'recipes',
      'entryBeingEdited': 0,
    };
  },

  methods: {
    'goRecipes': function () {
      this.page = "recipes";
    },
    'goAddRecipe': function () {
      this.page = "add";
    },
    'onNewEntryCreated': function () {
      this.page = "recipes";
    },
    'editEntry': function (entryId) {
      this.page = "edit";
      this.entryBeingEdited = entryId;
    },
  },  
};
</script>

<style>
</style>
