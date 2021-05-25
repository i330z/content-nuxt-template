<template>
  <div class="main-wrapper">
    <div class="container">
      <div class="row">
        <div class="col-md-8 offset-md-2">
          <app-search-input />

        </div>
      </div>
      <div class="row">
        <div class="col-md-4" v-for="article in articles" :key="article.title">
          <div class="card">
            <div class="card-img"></div>
            <div class="card-text">
              <h2>{{ article.title }}</h2>
              <n-link :to="article.slug">
                <button class="btn-default mt-3">VIEW</button>
              </n-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppSearchInput from '~/components/AppSearchInput.vue';
export default {
  components: { AppSearchInput },
  async asyncData ({ $content, params }){
    const articles = await $content('blog')
        .only(['title', 'description', 'slug', 'featured'])
        .sortBy('createdBy', 'asc')
        .fetch();

        return {
          articles
        }

  },

   jsonld() {
   
    return {
      "@context": "https://schema.org",
      "@type": "WebSite",
       "name": "NorthEast Nomads",
        "url": "https://northeastnomads-dev.web.app/",
        "potentialAction": {
          "@type": "SearchAction",
          "target": "{search_term_string}",
          "query-input": "required name=search_term_string"
    }
  }
}
}
</script>


<style scoped>
.main-wrapper{
  min-height: 100vh;
}
.blog-post-card{
  /* padding: 20px; */
  /* height: 200px; */
  /* border: 1px solid rgb(207, 207, 207); */
  margin-bottom: 20px;
  background: white;
}

.card{
  border: 1px solid var(--primary);

}

.card-text{
  padding: 20px;
}

/* .blog-post-card h2{
  font-size: 30px;
}

.blog-post-card p{
  color: #777;
}

.blog-post-img{
  width: 100%;
  height: 100%;
  background: red;
  object-fit: cover;
} */

</style>
