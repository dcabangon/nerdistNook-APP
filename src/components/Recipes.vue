<template> 
<h1>All Recipe</h1>
</template> 

<script>
const BASE_API_URL="https://3000-dcabangon-nerdistnookapi-xwxhxz2ave4.ws-us29.gitpod.io/"

import axios from 'axios'
export default{
    created: async function() {
        let response = await axios.get(BASE_API_URL +'/item_entry')
        console.log(response.data)
    }
}
</script>

