<template>
  <div>
    <a-button type="primary" size="large" @click="openModal">
      <b>Nova Task</b>
    </a-button>

    <a-modal v-model:visible="modalOpen" :width="600" title="Adicionar nova tarefa" @cancel="closeModal">
      <a-form @submit.prevent="submitForm" layout="vertical">
        <a-form-item label="Título da Tarefa" required>
          <a-input v-model="form.title" />
        </a-form-item>
        <a-form-item label="Descrição" required>
          <a-textarea v-model="form.description" />
        </a-form-item>
        <create-category-modal style="margin-bottom: 5px;" @category-created="fetchCategories" />
        <a-form-item label="Categorias">
          <a-select v-model="form.category_ids" mode="multiple" placeholder="Selecione">
            <a-select-option v-for="category in categoriesItems" :key="category.id" :value="category.id">
              {{ category.name }}
            </a-select-option>
          </a-select>
        </a-form-item>
      </a-form>
      <template #footer>
        <a-button @click="closeModal">Cancelar</a-button>
        <a-button type="primary" @click="submitForm">Salvar</a-button>
      </template>
    </a-modal>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import CreateCategoryModal from './CreateCategoryModal.vue'

export default {
  components: { CreateCategoryModal },
  data() {
    return {
      modalOpen: false,
      form: {
        title: '',
        description: '',
        status: 'BACKLOG',
        category_ids: [],
      },
      categoriesItems: [],
    }
  },
  computed: {
    ...mapState(['user']),
    categories() {
      return this.$store.state.categories
    },
    userId() {
      return this.user.id
    }
  },
  methods: {
    openModal() {
      this.modalOpen = true
      this.fetchCategories()
    },
    closeModal() {
      this.modalOpen = false
      this.resetForm()
    },
    resetForm() {
      this.form = {
        title: '',
        description: '',
        status: 'BACKLOG',
        category_ids: [],
        user_id: null,
      }
    },
    async submitForm() {
      try {
        await this.$store.dispatch('createCardStore', { 
          userId: this.userId, 
          cardForm: this.form,
        })
        this.closeModal()
      } catch (error) {
        console.error('Erro ao salvar tarefa:', error)
        alert('Erro ao salvar tarefa. Preencha os campos obrigatórios.')
      }
    },
    async fetchCategories() {
      try {
        await this.$store.dispatch('fetchCategoriesStore', this.userId)
        this.categoriesItems = this.categories.map(category => ({
          id: category.id,
          name: category.name,
        }))
      } catch (error) {
        console.error('Erro ao obter categorias:', error)
      }
    },
  },
}
</script>
