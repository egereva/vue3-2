<template>
  <form class="card card-w30" @submit.prevent="addBlock">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="valueInput"></textarea>
    </div>

    <app-button color="primary"
                :disabled="isDisabled"
                type="submit">Добавить</app-button>
  </form>
</template>

<script>
import AppButton from '@/components/ui/AppButton'
export default {
  emits: {
    'add-block'(type, value) {
      if (type && value) {
        return true
      }
      console.warn('Не хватает параметров для emit add-block')
      return false
    }
  },
  data() {
    return {
      type: 'title',
      valueInput: '',
    }
  },
  computed: {
    isDisabled() {
      return !(this.valueInput.length > 3)
    }
  },
  methods: {
    addBlock() {
      this.$emit('add-block', this.type, this.valueInput)

      this.resetForm()
    },
    resetForm() {
      this.type = 'title'
      this.valueInput = ''
    },
  },
  components: {
    AppButton
  }
}
</script>

<style scoped>

</style>
