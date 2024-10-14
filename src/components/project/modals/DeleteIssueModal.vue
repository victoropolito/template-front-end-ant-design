<template>
  <div>
    <a-button type="danger" icon="DeleteOutlined" shape="circle" @click="openModal" />

    <a-modal v-model:visible="modalOpen" :width="500" title="Excluir tarefa?" @cancel="modalOpen = false">
      <span>Deseja mesmo excluir a tarefa? Essa ação é irreversível!</span>
      <template #footer>
        <a-button @click="modalOpen = false">Cancelar</a-button>
        <a-button type="primary" danger @click="deleteCard">Excluir</a-button>
      </template>
    </a-modal>
  </div>
</template>

<script>
import { DeleteOutlined } from '@ant-design/icons-vue'

export default {
  components: {
    DeleteOutlined
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
    }
  },
  methods: {
    openModal() {
      this.modalOpen = true
    },
    async deleteCard() {
      const id = this.card.id;

      try {
        await this.$store.dispatch('deleteCardStore', id);
        this.modalOpen = false
        return true;
      } catch (error) {
        console.error('Error deleting card:', error);
        throw error;
      }
    },
  },
}
</script>
