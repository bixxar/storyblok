<template>
  <component
    :is="story.content.component"
    v-if="story.content.component"
    :key="story.content._uid"
    :blok="story.content"
  />
</template>

<script>
export default {
  asyncData(context) {
    const env = process.env.NODE_ENV || 'prod'
    const version =
      context.query._storyblok || env === 'dev' ? 'draft' : 'published'
    const fullSlug =
      context.route.path === '/' || context.route.path === ''
        ? 'home'
        : context.route.path
    return context.app.$storyapi
      .get(`cdn/stories/${fullSlug}`, {
        version,
        resolve_relations: 'featured-articles.articles',
      })
      .then((res) => {
        return res.data
      })
      .catch((res) => {
        if (!res.response) {
          console.error(res)
          context.error({
            statusCode: 404,
            message: 'Failed to receive content from API',
          })
        } else {
          console.error(res.response.data)
          context.error({
            statusCode: res.response.status,
            message: res.response.data,
          })
        }
      })
  },
  data() {
    return {
      story: { content: {} },
    }
  },
  mounted() {
    // Use the input event for the live update of content
    this.$storybridge.on('input', (event) => {
      if (event.story.id === this.story.id) {
        this.$storybridge.resolveRelations(
          ['featured-articles.articles'],
          (event) => {
            // event.story.content has now the resolved relations
            this.story.content = event.story.content
          }
        )
      }
    })

    // Use the birdge to listen the events
    this.$storybridge.on(['published', 'change'], (event) => {
      this.$nuxt.$router.go({
        path: this.$nuxt.$router.currentRoute,
        force: true,
      })
    })
  },
}
</script>

<style>
.app {
  margin: 0;
}
</style>
