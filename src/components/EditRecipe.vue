<template>
    <div>
        <h1>Edit Recipe</h1>
        <div>
            <label>Book Name</label>
            <input type="text" v-model="bookName" class="form-control"/>
        </div>
        <div>
            <label>Publisher</label>
            <input type="text" 
                   class="form-control"
                   placeholder="Seperate each ingredient with a comma"
                   v-model="publisher"/>
        </div>
        <button v-on:click="updateRecipe" class="my-3">Update</button>
    </div>
</template>

<script>
// BE SURE TO CHANGE THE API TO THE HEROKU VERSION WHEN YOU DEPLOYED YOUR VUE PROJECT
const BASE_API_URL="https://3000-dcabangon-nerdistnookapi-xwxhxz2ave4.ws-us29.gitpod.io/"
import axios from 'axios'
export default {
    data:function(){
        return {
            id:"",
            bookName: "",
            publisher:""
        }
    },
    created:async function() {
        let response = await axios.get(BASE_API_URL + "books/" + this.recipeId)
        console.log(response.data)
        let book = response.data.book;
        this.bookName = book.bookName;
        this.publisher = book.publisher;
        this.id = book.id;
    },
    
    props:['recipeId'],
    
     methods: {
        "updateRecipe":async function() {
            await axios.put(BASE_API_URL + "books" + this.recipeId,{
                'bookName': this.bookName,
                'publisher': this.publisher
            });
            
            this.$emit('recipe-updated')
        }
    }
}
</script>