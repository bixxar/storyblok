<template>
  <ul v-editable="blok" class="grid">
    <li v-for="item in blok.columns" :key="item._uid" clasys="d-flex px-4">
      <component :is="item.component" :blok="item" />
    </li>
  </ul>
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
.grid {
  display: flex;
}
</style>
