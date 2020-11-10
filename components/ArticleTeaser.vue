<template>
  <a class="d-block" href="#">
    <img :src="resizedImage" alt="image alt" class="pb-3" />
    <h2 class="pb-2">{{ articleContent.title }}</h2>
    <p class="pb-2">{{ articleContent.intro }}</p>
    <p class="">{{ articleContent.author }}</p>
  </a>
</template>

<script>
export default {
  props: {
    articleContent: {
      type: Object,
      required: true,
    },
  },
  computed: {
    resizedImage() {
      const imageUrl = this.articleContent.hero_image
      if (typeof imageUrl !== 'undefined') {
        return imageUrl.filename.replace(
          '//a.storyblok.com',
          '//img2.storyblok.com/300x250'
        )
      }

      return null
    },
  },
}
</script>

<style scoped>
.feature {
  font-weight: 700;
}
</style>
