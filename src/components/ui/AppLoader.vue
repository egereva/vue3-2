<template>
  <div class="loader" :class="color"></div>
</template>

<script>
export default {
  props: {
    color: String,
    default: '',
    validator(value) {
      return ['', 'black'].includes(value)
    }
  }
}
</script>
