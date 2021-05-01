<template>
  <div>
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
export default {
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

