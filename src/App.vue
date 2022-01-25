<template>
  <div class="container-fluid">
    <!-- NAVBAR -->
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <button v-on:click="goRecipes" class="nav-link active" aria-current="page">
          Recipes
        </button>
      </li>
      <li class="nav-item">
        <button v-on:click="goAddRecipe" class="nav-link">Add new</button>
      </li>
    </ul>
    <!-- END OF NAVBAR -->
    <div>
      <Recipes v-if="page ==='recipes'" />
      <AddRecipe v-if="page ==='add'" />
    </div>
  </div>
</template>

<script>
import AddRecipe from "@/components/AddRecipe";
import Recipes from "@/components/Recipes";

export default {
  name: "App",
  components: {
    Recipes,
    AddRecipe,
  },

  data: function () {
    return {
      page: "recipes",
    };
  },

  methods: {
    "goRecipes": function () {
      this.page = "recipes";
    },
    "goAddRecipe": function () {
      this.page = "add";
    },
  },
};
</script>

<style>
</style>
