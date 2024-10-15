<template>
  <a-col :span="8">
    <a-card class="box-card">
      <template #title>
        <div class="header clearfix">
          <h3>{{ statusLabel }}</h3>
          <span class="card-header-count">{{ cards.length }}</span>
        </div>
      </template>

      <a-card v-for="card in cards" :key="card.id" class="inner-card " hoverable>
        <template #title>
          <strong>{{ card.title }}</strong>
        </template>
        <div>
          <a-tag v-for="category in card.categories" :key="category.name" :color="category.color" class="tag-margin">
            {{ category.name }}
          </a-tag>
        </div>
        <div><i>{{ card.description }}</i></div>
        <div class="card-actions">
          <EditIssueModal :card="card" />
          <DeleteIssueModal :card="card" />
        </div>
      </a-card>
    </a-card>
  </a-col>
</template>

<script>
import EditIssueModal from './modals/EditIssueModal.vue';
import DeleteIssueModal from './modals/DeleteIssueModal.vue';

export default {
  components: { EditIssueModal, DeleteIssueModal },
  props: {
    statusLabel: {
      type: String,
      required: true
    },
    cards: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.box-card {
  margin: 10px;
  border-radius: 3px;
  padding: 10px;
  box-shadow: 0 0 1px black;
}

.inner-card {
  margin: 10px 0;
  box-shadow: 0 0 1px black;
}

.tag-margin {
  margin: 0 1px 1px 0;
}

.card-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.header {
  display: flex;
  justify-content: space-between;
}

.card-header-count {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: smaller;
  color: rgba(66, 66, 66, 0.664);
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: lightgray;
}
</style>
