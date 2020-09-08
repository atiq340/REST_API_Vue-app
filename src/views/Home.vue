<template>
  <div class="home">
    
    <AddPosts v-on:add-post="addPost"/>
    <PostList v-on:del-post="deletepost" v-bind:posts="posts"/>
    <h1>welcome home</h1>
    
    
  </div>
</template>


<script>
import axios from "axios"

import AddPosts from "@/views/AddPosts.vue"
import PostList from "@/views/PostList.vue"
// @ is an alias to /src


export default {
  name: "Home",
  components:{
    AddPosts,
    PostList
  },
  data(){
    return{
      posts:[],
      errors:[]
    }
  },
  methods:{
    addPost(newpost){
const {title,body}=newpost;
axios.post("https://jsonplaceholder.typicode.com/posts",{
  title,
  body
})
.then(res=>(
  this.posts=[...this.posts,res.data]
))
.catch(err=>console.log(err));
    },
    deletepost(id){
axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
.then(()=>
  this.posts=this.posts.filter(post=>post.id !==id))
.catch(err=>{
  console.log(err)
})
  }
  },
  created(){
    axios.get(`https://jsonplaceholder.typicode.com/posts?_limit=5`)
    .then(res =>{
      this.posts=res.data

    })
    .catch(e=>{
      this.errors.push(e)
    })
  },
  
  
}
</script>
