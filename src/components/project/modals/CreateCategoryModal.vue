<template>
  <div>
    <a-button @click="openModal" type="primary" size="small">
      <PlusOutlined />Criar nova categoria
    </a-button>

    <a-modal v-model:visible="modalOpen" :width="400" title="Criar nova categoria" @cancel="modalOpen = false">
      <a-form @submit.prevent="submitForm" layout="vertical">
        <a-form-item label="Nome da categoria" required>
          <a-input v-model="form.name" />
        </a-form-item>
        <a-form-item label="Cor da categoria" required>
          <a-color-picker v-model="form.color" />
        </a-form-item>
      </a-form>
      <template #footer>
        <a-button @click="modalOpen = false">Cancelar</a-button>
        <a-button type="primary" @click="submitForm">Salvar</a-button>
      </template>
    </a-modal>
  </div>
</template>

<script>
import { PlusOutlined } from '@ant-design/icons-vue'

export default {
  components: {
    PlusOutlined
  },
  data() {
    return {
      modalOpen: false,
      form: {
        name: '',
        color: ''
      }
    }
  },
  methods: {
    openModal() {
      this.modalOpen = true
    },
    async submitForm() {
      try {
        await this.$store.dispatch('createCategoryStore', this.form)
        this.modalOpen = false
        this.$emit('category-created')
      } catch (error) {
        console.error('Erro ao criar categoria:', error)
      }
    }
  }
}
</script>
