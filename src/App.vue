
<template>
  <div>
   <div class="container-fluid">
     <!-- navbar -->
     <ul class="nav nav-tabs">
       <li class="nav-item">
         <button v-on:click="goRecipes" class="nav-link active" aria-current="page">Recipes</button>
       </li>
       <li class="nav-item">
         <button v-on:click="goAddRecipe" class="nav-link">Add New</button>
       </li>
        <li class="nav-item">
         <button v-on:click="goAboutUs" class="nav-link">About Us</button>
       </li>
     </ul>
     <!-- end navbar -->
     
     <div>
       <Recipes v-if="page==='recipes'" v-on:update-recipe="editRecipe"/>
       <AddRecipe v-if="page==='add'" v-on:new-recipe-created="onNewRecipeCreated"/>
       <AboutUs v-if="page==='about-us'"/>
       <EditRecipe v-if="page==='edit'" v-bind:recipeId="recipeBeingEdited" v-on:recipe-updated="onRecipeUpdated"/>
       
     </div>
   </div>
 </div>
</template>

<script>
import AddRecipe from "@/components/AddRecipe"
import Recipes from "@/components/Recipes"
import AboutUs from "@/components/AboutUs"
import EditRecipe from "@/components/EditRecipe"
export default {
  name: 'App',
  components: {
     Recipes, AddRecipe, AboutUs, EditRecipe
  },
  data: function() {
    return {
      'page': 'recipes',
      'recipeBeingEdited': 0
    }
  },
  methods:{
    'goRecipes': function() {
      this.page = "recipes"
    },
    'goAddRecipe': function() {
      this.page = "add"
    },
    'goAboutUs': function() {
      this.page= "about-us"
    },
    'onNewRecipeCreated':function() {
      this.page="recipes"
    },
    'editRecipe': function(recipeId) {
      this.page="edit";
      this.recipeBeingEdited = recipeId;
      
    },
    'onRecipeUpdated':function() {
      this.page="recipes"
    }
  }
}
</script>

<style>
</style>