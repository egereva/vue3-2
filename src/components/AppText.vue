<template>
  <p>
    {{ value }}
  </p>
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
