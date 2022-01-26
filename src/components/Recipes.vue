<template>
  <div>
    <h1>All Recipe</h1>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Title</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="r in recipes" v-bind:key="r._id">
        <td>{{ r.bookName }}</td>
        <td>{{ r.publisher }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template> 

<script>
const BASE_API_URL =
  "https://3000-dcabangon-nerdistnookapi-xwxhxz2ave4.ws-us29.gitpod.io/";

import axios from "axios";
export default {
  created: async function () {
    let response = await axios.get(BASE_API_URL + "item_entry");
    this.recipes = response.data;
  },
  data: function () {
    return {
      recipes: [],
    };
  },
};
</script>

