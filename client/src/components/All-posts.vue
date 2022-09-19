<template>

  <div id="News" class="AllNews">
    <h1> All the News </h1>
    <button @click="getAll()"></button>
    <input type="text" v-model="search" placeholder="search"/>
    <div id="container"></div>
    <ul id="post" v-for=" (post,index) in fiteredposts" :key="index">
    <li>{{post.text}}</li>
    <br/>
    <img id="pictureofNews" v-bind:src="post.content"/>
    
    <br/>
    <li>{{post.id}}</li>
    </ul>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return{
      Allposts:[],
       search:"", 
    }
 
  },

  methods: {
    getAll() {
      axios.get('http://localhost:3000/getAll').then((result) => {this.Allposts=result.data;console.log(this.Allposts)}).catch((err) => console.log(err))
    }
  },
    computed:{
  fiteredposts:function (){
    return this.Allposts.filter((post)=>{return post.theme.match(this.search,)})
  }
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}

ul {
  display: inline-block;
  list-style-type: none;
  padding: 1% 1% 1% 1%;
  width:400px;
  height: 250px;
}

li {
  display: inline-block;
}

a {
  color: #42b983;
}

#pictureofNews{
  width: 300px;
  height: 200px;
}
#container{
  display :flex;
}
</style>
