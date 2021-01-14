<template>
  <h2>{{ value }}</h2>
</template>

<script>
export default {
  computed: {
    value() {
      return this.$attrs.value
    }
  }
}
</script>

<style scoped>

</style>
