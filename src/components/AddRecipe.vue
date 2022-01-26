<template>
  <div>
    <h1>Add Recipe</h1>

    <div>
      <label>Book Name</label>
      <input type="text" v-model="bookName" class="form-control"/>
    </div>

    <div>
      <label>Publisher</label>
      <input
        type="text"
        class="form-control"
        placeholder="Seperate each ingredient with a comma"
        v-model="publisher"/>
    </div>
    <button v-on:click="addNew">Add New</button>
  </div>
</template> 


<script>
export default {
  data: function () {
    return {
      bookName: "",
      publisher: "",
    };
  },
};
</script>
