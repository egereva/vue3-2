<template>
  <h1>{{ value }}</h1>
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
