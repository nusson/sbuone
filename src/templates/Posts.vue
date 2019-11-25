<!-- eslint-disable -->
<docs>
# PostSingle
> Single post

@author Nicolas Husson <hello@nusson.ninja>
</docs>
<!-- eslint-enable -->

<script>
export default {
  name: 'PostSingle',
  computed:{
    data(){ return this.$page.node },
    title(){ return this.data.title },
    content(){ return this.data.content },
    thumbnail(){ return this.data.thumbnail },
  },
  components: {},
  props: {},
  data(){
    return {}
  },
  mounted() {},
  methods: {},
};
</script>

<template>
  <Layout>
    <article class="article -single">
      <header class="head">
        <g-image :src="thumbnail" width="300" class="thumbnail"/>
        <h2 class="title" v-text="title"></h2>
      </header>
      <div class="content _wysiwyg" v-html="content"></div>
    </article>
  </Layout>
</template>


<style scoped>

.article{
  position: relative;
}
.head{
  display: block;
}
.thumbnail{
  display: inline-block;
  width: 500px;
  height: 200px;
  position: relative;
  object-fit: cover;
}
.title{
  position: relative;
  z-index: 2;
}
</style>

<page-query>
# Write your query or mutation here
query($path:String!="/posts/test"){
  node:post(path:$path){
    title
    excerpt
    thumbnail
    date
    id
    timeToRead
    content
  }
}
</page-query>