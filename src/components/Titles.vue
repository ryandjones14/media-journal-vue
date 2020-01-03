<template>
  <div>
    <li v-for="title in titles" v-bind:key="title.id">
      {{ title.title }}
    </li>
  </div>
</template>

<script>
export default {
  name: 'Titles',
  props: {
    titles: Array,
  },
}
</script>

<style scoped>

</style>