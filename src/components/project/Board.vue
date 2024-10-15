<template>
  <a-layout class="board-layout">
    <a-row :gutter="10">
      <card-column :status-label="'Não iniciado'" :cards="filteredCards('BACKLOG')" />
      <card-column :status-label="'Em Progresso'" :cards="filteredCards('IN PROGRESS')" />
      <card-column :status-label="'Concluído'" :cards="filteredCards('COMPLETED')" />
    </a-row>
  </a-layout>
</template>

<script>
import CardColumn from './CardColumn.vue'

export default {
  components: { CardColumn },
  props: {
    userId: {
      type: String,
      required: true
    },
  },
  computed: {
    cards() {
      return this.$store.state.cards
    },
  },
  mounted() {
    if (!this.cards.length) {
      this.fetchCards()
    }
  },
  methods: {
    async fetchCards() {
      try {
        const user_id = this.userId;
        await this.$store.dispatch('fetchCardsAction', user_id);
      } catch (error) {
        console.error('Error fetching cards:', error);
      }
    },
    filteredCards(status) {
      return this.cards.filter(card => card.status === status);
    }
  },
}
</script>

<style scoped>
.board-layout {
  justify-content: flex-start;
  padding: 10px;
  margin: 10px 20px 5px 10px;
}
</style>