<template>
  <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">ProductName</th>
      <th scope="col">Delete</th>
      <th scope="col">Update</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(post,index) in posts" :key="index">
      <th scope="row">{{index+1}}</th>
      <td>{{post.name}}</td>
     
      <td><button @click="deleteUsers(post._id)" type="button" class="btn btn-danger">Delete</button></td>
      <td><button  type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal">Update</button></td>
      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
           <input v-model="reName" type="text" class="form-control" id="text" aria-describedby="name">
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" @click="updateUsers(post._id)">Save changes</button>
      </div>
    </div>
  </div>
</div>
    </tr>
  
  </tbody>
</table>

<div v-if="errors">{{errors}}</div>
</template>

<script>
import axios from 'axios'
import {ref} from 'vue'

export default {
    data() {
        return {
            
        }
    },
    setup() {
        const posts = ref([])
        const errors = ref(null)
        const reName = ref(null)
      

        const loadingPosts = async()=>{
          try {
                let post = await fetch("http://localhost:5000/admin/getAllProducts")
            posts.value = await post.json()
            console.log(posts.value)

            if(!post.ok){
                throw new Error("verilere erişilemedi")
            }
          
              
          } catch (error) {
              errors.value = error.message
              
          }

        }
        const deleteUsers = async(id)=>{
            try {
               await axios.delete("http://localhost:5000/admin/delete/"+id)
                window.location.reload()
         
                
            } catch(error) {
                throw new Error("hata")
                
            }
        }
        const updateUsers = async(id)=>{
            try{
              await axios.put(`http://localhost:5000/admin/update/${id}`,{
                  name:reName.value
              }

              
                )
                window.location.reload()
                console.log(reName.value)
              

            }
            catch(error){
                throw new Error("hata")
            }
        }
      
        loadingPosts()
     
   

        return{posts,errors,deleteUsers,updateUsers,reName}
        
    }
}

</script>

<style>
.table{
   margin-top:40px 
}

</style>