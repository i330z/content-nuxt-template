<template>
    <div>
        <nuxt-img :src="featured.img" :alt="featured.alt" class="featured-image" fit="cover" sizes="sm:100vw md:50vw lg:400px" quality="50" format="webp" loading="lazy" />
    </div>
</template>

<script>
  export default {
    props: {
      featured: {
        type: Object,
        required: true
      }
    }
  }
</script>


<style scoped>
.featured-image{
    width: 100%;
    /* object-fit: cover; */
}
</style>