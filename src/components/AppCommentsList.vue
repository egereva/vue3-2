<template>
  <ul class="list" v-if="comments.length">
    <li class="list-item" v-for="comment in comments" :key="comment.id">
      <div>
        <p><strong>{{ comment.email }}</strong></p>
        <small>{{ comment.body }}</small>
      </div>
    </li>
  </ul>
  <p v-else>Комментариев пока нет</p>
</template>

<script>
export default {
  props: {
    comments: {
      type: Array,
      require: true
    }
  }
}
</script>

<style scoped>

</style>
