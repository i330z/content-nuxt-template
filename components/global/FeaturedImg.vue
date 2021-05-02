<template>
    <div>
        <img :src="featured.img" :alt="featured.alt" class="featured-image">
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
    object-fit: cover;
}
</style>