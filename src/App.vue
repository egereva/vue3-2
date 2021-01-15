<template>
  <div class="container column">
    <app-form @add-block="addBlock"></app-form>

    <div class="card card-w70">
      <template v-if="blocks.length" v-for="element in blocks">
        <component :is="element.component" v-bind="{ value: element.value }"></component>
      </template>

      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>

  </div>

  <div class="container">
    <p>
      <app-button color="primary" @action="loadComments">Загрузить комментарии</app-button>
    </p>

    <template v-if="showComments">
      <app-loader v-if="loading"></app-loader>
      <div class="card" v-else>
        <h2>Комментарии</h2>
        <app-comments-list :comments="comments"></app-comments-list>
      </div>
    </template>

  </div>
</template>

<script>
import AppTitle from '@/components/AppTitle'
import AppSubtitle from '@/components/AppSubtitle'
import AppAvatar from '@/components/AppAvatar'
import AppText from '@/components/AppText'
import AppCommentsList from '@/components/AppCommentsList'
import AppLoader from '@/components/ui/AppLoader'
import AppButton from '@/components/ui/AppButton'
import AppForm from '@/components/AppForm'
import axios from 'axios'

export default {
  data() {
    return {
      blocks: [],
      comments: [],
      loading: false,
      showComments: false
    }
  },
  mounted() {
    this.loadBlocks()
  },
  methods: {
    async loadBlocks() {
      try{
        const {data} = await axios.get('https://vue3-2-default-rtdb.firebaseio.com/resume.json')

        this.blocks = Object.keys(data).map(key => {
          return {
            id: key,
            ...data[key]
          }
        })

      } catch (e) {
        console.log(e.message)
      }
    },
    async addBlock(type, value) {
      const response = await axios.post('https://vue3-2-default-rtdb.firebaseio.com/resume.json', {
        component: `app-${type}`,
        value: value
      })

      const firebaseData = await response.data

      this.blocks.push({
        component: `app-${type}`,
        value: value,
        id: firebaseData.name
      })

    },

    async loadComments() {
      this.showComments = true
      try {
        this.loading = true
        const response = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
        this.comments = response.data
        this.loading = false
      } catch (e) {
        console.log(e.message)
      }
    }
  },
  components: {
    AppTitle,
    AppSubtitle,
    AppAvatar,
    AppText,
    AppCommentsList,
    AppLoader,
    AppButton,
    AppForm
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
