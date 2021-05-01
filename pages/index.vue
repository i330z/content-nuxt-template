<template>
  <div style="width:800px; margin:0 auto; margin:50px auto">

    <app-search-input />
    <div v-for="article in articles" :key="article.slug">
      <n-link :to="article.slug">
        <div>
          <h1>{{ article.title }}</h1>
          <p>{{ article.description }}</p>
        </div>
      </n-link>  
    </div>
  </div>
</template>

<script>
import AppSearchInput from '~/components/AppSearchInput.vue';
export default {
  components: { AppSearchInput },
  async asyncData ({ $content, params }){
    const articles = await $content('blog')
        .only(['title', 'description', 'slug'])
        .sortBy('createdBy', 'asc')
        .fetch();

        return {
          articles
        }

  }
}
</script>

