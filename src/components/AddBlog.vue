<template>
    <div id="add-blog">
        <h1 v-if="!submitted">添加博客</h1>
        <h1 v-if="submitted">博客发布成功</h1>
        <form v-if="!submitted">
          <label>标题</label>
          <input type="text" v-model="blog.title"/>
          <label>内容</label>
          <textarea v-model="blog.content"></textarea>
          <div id="categories">
            <label>vuejs</label>
            <input type="checkbox" v-model="blog.categories" value="vuejs"/>
            <label>angularjs</label>
            <input type="checkbox" v-model="blog.categories" value="angularjs"/>
            <label>java</label>
            <input type="checkbox" v-model="blog.categories" value="java"/>
            <label>react</label>
            <input type="checkbox" v-model="blog.categories" value="react"/>
          </div>
          <label>作者</label>
          <select v-model="blog.author">
            <option v-for="author in authors">{{author}}</option>
          </select>
          <button v-on:click.prevent="post">发布博客</button>
        </form>
    <!-- <div id="preview">
      <h1>博客总览</h1>
      <p>标题 : {{blog.title}}</p>
      <p>内容 ： </p>
      <p>{{blog.content}}</p>
      <p>分类</p>
      <p>
        <ul>
          <li v-for="category in blog.categories">{{category}}</li>
        </ul>
      </p>
      <p>作者 ： {{blog.author}}</p>
    </div> -->
    </div>
</template>

<script>
export default {
  name: 'add-blog',
  data () {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: ""
      },
      authors: ["John" , "Lisa" , "Henry"],
      submitted: false
    }
  },
  methods:{
    post:function(){
      this.$http.post('http://jsonplaceholder.typicode.com/posts',{
          title: this.blog.title,
          body: this.blog.content,
          userId : 1
      }).then(function(data){
        this.submitted=true;
        console.log(data);
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog *{
  box-sizing: border-box;
}

#add-blog{
  margin: 20px auto;
  max-width: 600px;
  padding: 20px; 
}

label{
  display: block;
  margin: 20px 0 10px;
}

input[type="text"],textarea, select {
  display: block;
  width: 100%;
  padding: 8px;
}

select{
  padding: 4px;
  width: 200px;
}

textarea{
  height: 300px;
}

#categories label{
  display: inline-block;
  margin-top: 8px;
}
#categories input{
  display: inline-block;
  margin-right: 10px;
}

button{
  display: block;
  margin: 20px 0;
  background: crimson;
  color: #fff;
  border: 0;
  padding: 10px;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
}
</style>
