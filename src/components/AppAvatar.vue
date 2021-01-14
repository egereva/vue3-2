<template>
  <div class="avatar">
    <img :src="value">
  </div>
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
