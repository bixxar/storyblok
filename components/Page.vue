<template>
  <div v-editable="blok" class="page">
    <component
      :is="section.component"
      v-for="section in blok.body"
      :key="section._uid"
      :blok="section"
    />
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
.page {
  background-color: grey;
}
</style>
