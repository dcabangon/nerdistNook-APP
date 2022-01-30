<template>
    <div>
        <h1>Add Recipe</h1>
        <div>
            <label>Book Name</label>
            <input type="text" v-model="bookName" class="form-control"/>
        </div>
        <div>
            <label>publisher</label>
            <input type="text" 
                   class="form-control"
                   placeholder="Seperate each ingredient with a comma"
                   v-model="publisher"/>
        </div>
        <button v-on:click="addNew" class="my-3">Add New</button>
    </div>
</template>

<script>
const BASE_API_URL="https://3000-dcabangon-nerdistnookapi-7e4pnbeivwk.ws-us29.gitpod.io/"
import axios from 'axios'
export default {
    data:function(){
        return {
            id:"",
            bookName: "",
            publisher:""
        }
    },
    methods: {
        "addNew":async function() {
            await axios.post(BASE_API_URL + "books",{
                'bookName': this.bookName,
                'publisher': this.publisher
            });
            this.$emit('new-recipe-created')
        }
    }
}
</script>