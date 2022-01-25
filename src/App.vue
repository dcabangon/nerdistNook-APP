<template>
  <div class="container-fluid">
    <!-- NAVBAR -->
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <button class="nav-link active" aria-current="page">Recipes</button>
      </li>
      <li class="nav-item">
        <button class="nav-link">Add new</button>
      </li>
    </ul>
    <!-- END OF NAVBAR -->
    <div>
      <Recipes/>
      <AddRecipe/>
    </div>
  </div>
</template>

<script>
import AddRecipe from "@/components/AddRecipe"
import Recipes from "@/components/Recipes";

export default {
  name: "App",
  components: {
    Recipes, AddRecipe
  },
};
</script>

<style>
</style>
