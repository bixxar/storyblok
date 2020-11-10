<template>
  <div v-editable="blok" class="feature text-center">
    <h2>{{ blok.name }}</h2>
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
.feature {
  font-weight: 700;
}
</style>
