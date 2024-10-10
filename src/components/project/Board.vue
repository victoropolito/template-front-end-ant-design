<template>
  <a-row gutter={16} justify="center" class="mb-6">
    <a-col :span="8">
      <a-card title="Não iniciado" bordered={false} class="column">
        <template #extra>
          TAMANHO backlog
        </template>
        <a-card
          v-for="n in 5"
          :key="n"
          class="pa-3 ma-2"
          title="TITULO CARD"
          hoverable
        >
          <div>
            <a-tag
              class="ma-1"
            >
              NOME CATEGORIA
            </a-tag>
          </div>
          <p><i>DESCRICAO CARD</i></p>
          <a-space>
            <!-- <edit-issue-modal :card="card" />
            <delete-issue-modal :card="card" /> -->
          </a-space>
        </a-card>
      </a-card>
    </a-col>

    <a-col :span="8">
      <a-card title="Em Progresso" bordered={false} class="column">
        <template #extra>
          TAMANHO in progress
        </template>
        <a-card
          v-for="n in 5"
          :key="n"
          class="pa-3 ma-2"
          title="TITULO CARD"
          hoverable
        >
          <div>
            <a-tag
              class="ma-1"
            >
              NOME CATEGORIA
            </a-tag>
          </div>
          <p><i>DESCRICAO CARD</i></p>
          <a-space>
            <!-- <edit-issue-modal :card="card" />
            <delete-issue-modal :card="card" /> -->
          </a-space>
        </a-card>
      </a-card>
    </a-col>

    <a-col :span="8">
      <a-card title="Concluído" bordered={false} class="column">
        <template #extra>
          TAMANHO COMPLETED
        </template>
        <a-card
          v-for="n in 5"
          :key="n"
          class="pa-3 ma-2"
          title="TITULO CARD"
          hoverable
        >
          <div>
            <a-tag
              class="ma-1"
            >
              NOME CATEGORIA
            </a-tag>
          </div>
          <p><i>DESCRICAO CARD</i></p>
          <a-space>
            <!-- <edit-issue-modal :card="card" />
            <delete-issue-modal :card="card" /> -->
          </a-space>
        </a-card>
      </a-card>
    </a-col>
  </a-row>
</template>

<script>
// import DeleteIssueModal from './project/modals/DeleteIssueModal.vue';
// import EditIssueModal from './project/modals/EditIssueModal.vue'

export default {
  // components: { EditIssueModal, DeleteIssueModal },
  // props: {
  //   userId: {
  //     type: String,
  //     required: true
  //   },
  // },
  // computed: {
  //   cards() {
  //     return this.$store.state.cards
  //   },
  // },
  // mounted() {
  //   if (!this.cards.length) {
  //     this.fetchCards()
  //   }
  // },
  // methods: {
  //   async fetchCards() {
  //     try {
  //       const user_id = this.userId
  //       await this.$store.dispatch('fetchCardsAction', user_id)
  //     } catch (error) {
  //       console.error('Error fetching cards:', error)
  //     }
  //   },
  //   filteredCards(status) {
  //     return this.cards.filter(card => card.status === status)
  //   },
  // },
}
</script>

<style scoped>
.column {
  background-color: rgba(255, 255, 255, 0.932);
  justify-content: flex-start;
  border-radius: 3px;
  padding: 10px;
  margin: 10px 20px 5px 10px;
  box-shadow: 0 0 1px black;
}
</style>
