<template>
  <div>
    <h1>Edit</h1>

    <div>
      <label>Book Name</label>
      <input type="text" v-model="bookName" class="form-control" />
    </div>

    <div>
      <label>Publisher</label>
      <input
        type="text"
        class="form-control"
        placeholder="Seperate each ingredient with a comma"
        v-model="publisher"/>
    </div>
    <button v-on:click="updateEntry" class="my-3">Add New</button>
  </div>
</template> 


<script>
const BASE_API_URL =
  "https://3000-dcabangon-nerdistnookapi-xwxhxz2ave4.ws-us29.gitpod.io/";

import axios from "axios";

export default {
  data: function () {
    return {
      id: "",
      bookName: "",
      publisher: "",
    };
  },
  created: async function () {
    let response = await axios.get(BASE_API_URL + "item_entry/" + this.entryId) 
    this.bookName = response.data.bookName;
    this.publisher = response.data.publisher;
    this.id = response.data_id;
  },
  props: ['entryId'],
  methods: {
    "updateEntry": async function () {
      await axios.post(BASE_API_URL + "item_entry", + this.entryId, {
        'bookName': this.bookName,
        'publisher': this.publisher,
      });
      this.$emit("entry-updated");
    },
  }, 
};
</script>
