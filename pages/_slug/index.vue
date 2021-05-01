<template>
    <div style="width:800px; margin: 0 auto;">
        blog article
        <nav>
            <ul>
                <li v-for="link of article.toc" :key="link.id" >
                <NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink>
                </li>
            </ul>
        </nav>
        <nuxt-content :document="article" />
    </div>
</template>


<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('blog', params.slug).fetch()

      return { article }
    }
  }
</script>


<style>
  .nuxt-content h2 {
    font-weight: bold;
    font-size: 28px;
    color: green;
    margin-bottom: 20px;
  }
  .nuxt-content h3 {
    font-weight: bold;
    font-size: 22px;
    margin-bottom: 20px;
  }
  .nuxt-content p {
    margin-bottom: 20px;
    line-height: 30px;
  }
</style>