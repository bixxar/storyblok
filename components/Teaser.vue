<template>
  <div v-editable="blok" class="article-teaser text-center">
    <h2>{{ blok.headline }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    blok: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped>
.article-teaser {
  color: white;
}
</style>
