<template>
    <div class="my-5">
       
        <div class="container-fluid px-50">
          <div class="row">
            <div class="col-md-8 col-12 bg-white" >
            <h1>{{ article.title }}</h1>
               <div class="toc">
                  <nav>
                      <ul>
                          <li v-for="link of article.toc" :key="link.id" >
                          <NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink>
                          </li>
                      </ul>
                  </nav>
                </div>
              <nuxt-content :document="article" />
            </div>
            <div class="col-md-4 col-12" >
              Ads
            </div>
          </div>
        </div>
    </div>
</template>


<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('blog', params.slug).fetch()

      return { article }
    },

    head() {
    return {
      title: this.article.title,
      meta: [
        {
          hid: "description",
          name: "description",
          content: this.article.description,
        },
      ],
      link: [
        {
          rel: "canonical",
          href: "https://nuxt-blog-template.com/" + this.article.dir,
        },
      ],
    };
  },
  }
</script>


<style>

  h1{
    font-size: 32px;
    margin-bottom: 20px;
  }
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

  ul{
    margin: 0px;
    padding: 0px;
  }

  ul > li{
   padding-bottom: 20px;
  }

  .toc{
    padding: 20px 40px;
    background: rgb(212, 252, 212);
    display: block;
    margin: 10px 0px;
  }
</style>