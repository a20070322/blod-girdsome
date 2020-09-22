<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" :style="`background-image: url('${GRIDSOME_API_URL+general.node.cover.url}')`">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{general.node.title}}</h1>
              <span class="subheading">{{general.node.subTitle}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.post.edges" :key="edge.node.id">
            <g-link :to="`/post/${edge.node.id}`">
              <h2 class="post-title">{{edge.node.title}}</h2>
            </g-link>
            <a href="post.html">
              <!-- <h3 class="post-subtitle">Problems look mighty small from 150 miles up</h3> -->
            </a>
            <p class="post-meta">
              Posted by {{edge.node.created_by.firstname}} {{edge.node.created_by.lastname}}
              <a
                href="#"
              >{{edge.node.title}}</a>
              on {{edge.node.created_at}}
            </p>
            <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="`/tag/${tag.id}`">{{tag.title}}</g-link>&nbsp;&nbsp;
              </span>
            </p>
            <hr />
          </div>

          <!-- Pager -->
          <Pager :info="$page.post.pageInfo" />
          <!-- <div class="clearfix">
            <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
          </div>-->
        </div>
      </div>
    </div>
    <hr />
  </Layout>
</template>
<page-query>
query($page:Int){
  post:allStrapiPost(perPage:1,page:$page)@paginate{
    pageInfo {
      totalPages
      currentPage
    }
    edges{
      node{
        id
        title
        created_by{
          id
          lastname
          firstname
        }
        tags{
          title
          id
        }
        created_at
      }
    }
  }
  allStrapiGeneral{
    edges{
      node{
        id
        title
        subTitle
        cover{
          url
        }
      }
    }
  }
}
</page-query>
<script>
import { Pager } from "gridsome";
export default {
  name: "IndexPage",
  metaInfo: {
    title: "Hello, world!",
  },
  computed:{
    general(){
      return this.$page.allStrapiGeneral.edges[0]
    }
  },
  components: {
    Pager,
  },
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
