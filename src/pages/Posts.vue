<!-- eslint-disable -->
<docs>
# PostsCollection
> 

@author Nicolas Husson <hello@nusson.ninja>
</docs>
<!-- eslint-enable -->

<script>
import {flow, map} from 'lodash'
export default {
  name: 'PostsCollection',
  computed:{
    entries(){
      console.log('posts', this.$page);
      return flow(
        ({posts})=>posts.edges,
        entries=>map(entries, ({node})=>node)
      )(this.$page)
    }
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
    <div class="PostsCollection">
      <ul class="list">
        <li class="item" v-for="({title, path, id, thumbnail, excerpt}) in entries" :key="`post-${id}`">
          <g-link tag="article" :to="path" class="article">
            <header class="header">
              <g-image :src="thumbnail" width="300" class="thumbnail"/>
              <h2 class="title" v-text="title"></h2>
            </header>
            <div class="content">
              <p class="excerpt" v-text="excerpt"></p>
            </div>
          </g-link>
        </li>
      </ul>
    </div>
  </Layout>
</template>

<style scoped>
p, h2, header{
  margin: 0;
  padding: 0;
}
.list{
  list-style: none;
}
.article{
  width: 200px;
  height: 200px;
  position: relative;
  display: flex;
  justify-content: flex-end;
  flex-direction: column;
  padding: 20px;
}
.title,
.content{
  position: relative;
  z-index: 2;
}
.header{
  flex-grow: 1;
  display: flex;
  align-items: flex-end;
}
.title{
  flex-grow: 1;
}
.thumbnail{
  display: inline-block;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  object-fit: cover;
  height: 100%;
}
</style>

<page-query>
query{
  posts : allPosts{
    edges{
      node{
        id
        path
        title
        thumbnail (width:200)
        excerpt
      }
    }
  }
}
</page-query>