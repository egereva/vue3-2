<template>
  <button class="btn" :class="color"
          :type="type"
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
    },
    type: {
      type: String,
      default: 'button',
      validator(value) {
        return ['button', 'reset', 'submit'].includes(value)
      }
    }
  }
}
</script>

<style scoped>

</style>
