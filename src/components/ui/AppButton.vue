<template>
  <button class="btn" :class="color"
          :disabled="disabled"
          @click="$emit('action')">
    <slot/>
  </button>
</template>

<script>
export default {
  emits: ['action'],
  props: {
    color: {
      type: String,
      default: '',
      validator(value) {
        return ['', 'primary', 'danger'].includes(value)
      }
    },
    disabled: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>

</style>
