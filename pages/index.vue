<template>
  <div class="main-wrapper">
    <div class="container">
      <div class="row">
        <div class="col-md-8 offset-md-2 col-12">
          <app-search-input />
          {{ articles.fetured }}
          <div v-for="article in articles" :key="article.slug">
            
              <div class="blog-post-card">
                <div class="row">
                  <div class="col-md-4">
                    <img :src="article.featured.img" :alt="article.featured.alt" class="blog-post-img">
                  </div>
                  <div class="col-md-8">
                    <div class="p-2">
                      <h2 class="mb-2">{{ article.title }}</h2>
                      <p>{{ article.description }}</p>
                      <n-link :to="article.slug">
                        <button class="btn-default mt-3">VIEW POST</button>
                      </n-link> 
                    </div>
                  </div>
                </div>
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

.blog-post-card h2{
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
}

</style>
