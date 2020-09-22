<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>#{{$page.tag.title}}</h1>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.tag.posts" :key="edge.id">
            <g-link :to="`/post/${edge.id}`">
              <h2 class="post-title">{{edge.title}}</h2>
            </g-link>
            <a href="post.html">
              <!-- <h3 class="post-subtitle">Problems look mighty small from 150 miles up</h3> -->
            </a>
            <p class="post-meta">
              <!-- Posted by {{edge.created_by.firstname}} {{edge.created_by.lastname}} -->
              <a
                href="#"
              >{{edge.title}}</a>
              on {{edge.created_at}}
            </p>
            <p>
              <!-- <span v-for="tag in edge.tags" :key="tag.id">
                <g-link :to="`/tag/${tag.id}`">{{tag.title}}</g-link>&nbsp;&nbsp;
              </span> -->
            </p>
            <hr />
          </div>

          <!-- Pager -->
          <!-- <Pager :info="$page.post.pageInfo" /> -->
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
query($id:ID!){
  tag:strapiTag(id:$id){
    id
    title
    posts{
      id
      title
      created_at
    }
  }
}
</page-query>

<script>
export default {
  name: "TagPage",
};
</script>

<style>
</style>