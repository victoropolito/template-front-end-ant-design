<template>
  <div>
    <a-button type="primary" size="large" @click="openModal">
      Nova Task
    </a-button>
    <!-- <a-modal
      v-model:visible="modalOpen"
      title="Adicionar Nova Tarefa"
      :footer="null"
      centered
    >
      <a-form @submit.prevent="submitForm">
        <a-form-item label="Título da Tarefa" :labelCol="{ span: 24 }" :wrapperCol="{ span: 24 }" required>
          <a-input v-model:value="form.title" placeholder="Título da Tarefa" />
        </a-form-item>
        <a-form-item label="Descrição" :labelCol="{ span: 24 }" :wrapperCol="{ span: 24 }" required>
          <a-textarea v-model:value="form.description" placeholder="Descrição" />
        </a-form-item>
        <a-form-item label="Categorias" :labelCol="{ span: 24 }" :wrapperCol="{ span: 24 }">
          <create-category-modal />
          <a-select
            v-model:value="form.category_ids"
            mode="multiple"
            allowClear
            placeholder="Selecione as categorias"
          >
            <a-select-option v-for="category in categoriesItems" :key="category.id" :value="category.id">
              NOME DA CATEGORIA
            </a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item label="Usuário" :labelCol="{ span: 24 }" :wrapperCol="{ span: 24 }" required>
          <a-select v-model:value="form.user_id" placeholder="Selecione o usuário">
            <a-select-option v-for="user in users" :key="user" :value="user">
              {{ user }}
            </a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item :wrapperCol="{ span: 24 }">
          <a-space>
            <a-button @click="closeModal">Cancelar</a-button>
            <a-button type="primary" htmlType="submit">Salvar</a-button>
          </a-space>
        </a-form-item>
      </a-form>
    </a-modal> -->
  </div>
</template>

<script>
// import CreateCategoryModal from './CreateCategoryModal.vue'

// export default {
//   components: { CreateCategoryModal },
//   data() {
//     return {
//       modalOpen: false,
//       form: {
//         title: '',
//         description: '',
//         status: 'BACKLOG',
//         category_ids: [],
//         user_id: '',
//       },
//       categoriesItems: [],
//       users: ['664270c9472c3c191f2576e1', 'Usuário 2', 'Usuário 3'],
//     }
//   },
//   computed: {
//     categories() {
//       return this.$store.state.categories
//     }
//   },
//   methods: {
//     openModal() {
//       this.modalOpen = true
//       this.fetchCategories()
//     },
//     closeModal() {
//       this.modalOpen = false
//       this.resetForm()
//     },
//     resetForm() {
//       this.form = {
//         title: '',
//         description: '',
//         status: 'BACKLOG',
//         category_ids: [],
//         user_id: '',
//       }
//     },
//     async submitForm() {
//       try {
//         await this.$store.dispatch('createCardStore', {
//           userId: this.form.user_id,
//           cardForm: this.form,
//         })
//         this.closeModal()
//       } catch (error) {
//         console.error('Erro ao salvar tarefa:', error)
//         alert('Erro ao salvar tarefa. Tente novamente.')
//       }
//     },
//     async fetchCategories() {
//       try {
//         await this.$store.dispatch('fetchCategoriesStore', '664270c9472c3c191f2576e1')
//         this.categoriesItems = this.categories.map(category => ({
//           id: category.id,
//           name: category.name,
//         }))
//       } catch (error) {
//         console.error('Erro ao obter categorias:', error)
//       }
//     },
//   },
// }
</script>