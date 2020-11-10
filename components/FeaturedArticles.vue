<template>
  <div v-editable="blok" class="py-3 mb-6">
    <h2>{{ blok.title }}</h2>
    <ul class="d-flex mx-3">
      <li v-for="article in blok.articles" :key="article._uid" class="">
        <article-teaser
          v-if="article.content"
          :article-content="article.content"
        />
      </li>
    </ul>
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
