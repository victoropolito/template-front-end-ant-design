<template>
  <div>
    <a-button type="primary" @click="openModal">
      <EditOutlined />
    </a-button>

    <a-modal v-model:visible="modalOpen" :width="600" title="Editar Tarefa" @cancel="closeModal">
      <a-form @submit.prevent="submitForm" layout="vertical">
        <a-form-item label="Novo título" required>
          <a-input v-model:value="editCard.title" />
        </a-form-item>
        <a-form-item label="Nova descrição" required>
          <a-textarea v-model:value="editCard.description" />
        </a-form-item>
        <a-form-item label="Novo status" required>
          <a-select v-model:value="editCard.status" placeholder="Selecione">
            <a-select-option v-for="status in allStatus" :key="status" :value="status">
              {{ status }}
            </a-select-option>
          </a-select>
        </a-form-item>
        <div class="category-modal-container">
          <create-category-modal @category-created="fetchCategories" />
        </div>
        <a-form-item label="Categorias">
          <a-select v-model:value="editCard.category_ids" mode="multiple" placeholder="Selecione">
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
import { EditOutlined } from '@ant-design/icons-vue'
import { mapState } from 'vuex'
import CreateCategoryModal from './CreateCategoryModal.vue'

export default {
  components: {
    EditOutlined, CreateCategoryModal
  },
  props: {
    card: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      modalOpen: false,
      editCard: {
        title: '',
        description: '',
        status: '',
        category_ids: []
      },
      allStatus: ['BACKLOG', 'IN PROGRESS', 'COMPLETED'],
      categoriesItems: []
    }
  },
  computed: {
    ...mapState(['user']),
    userId() {
      return this.user.id
    },
    categories() {
      return this.$store.state.categories
    },
  },
  methods: {
    openModal() {
      this.modalOpen = true
      this.fetchCategories()
      this.editCard = { ...this.card }
    },
    closeModal() {
      this.resetForm()
      this.modalOpen = false
    },
    resetForm() {
      this.editCard = {
        title: '',
        description: '',
        status: '',
        category_ids: []
      }
    },
    async submitForm() {
      const id = this.card.id

      try {
        await this.$store.dispatch('editCard', { cardId: id, updatedCardData: { ...this.editCard, user_id: this.userId } })
        this.closeModal()
        return true
      } catch (error) {
        throw error
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
