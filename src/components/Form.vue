<template>
 <form>
  <div class="mb-3 mt-3">
    <label for="exampleInputEmail1" class="form-label">Product Name</label>
    <input v-model="name" type="text" class="form-control" id="text" aria-describedby="name">
  
  </div>

  <button type="submit" @click="handleSubmit()" class="btn btn-primary">Add</button>
</form>
</template>

<script>
import axios from "axios"

export default {
    data() {
        return {
            name:""
        }
    },
    methods: {
        handleSubmit(){
            axios.post(`http://localhost:5000/admin/addproduct`,{
                name:this.name
            }).then(resp=>console.log(resp))
           
        }
    },

}
</script>

<style>

</style>