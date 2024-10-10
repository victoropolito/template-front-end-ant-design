<template>
  <a-row align="middle" justify="space-between" class="mb-6" style="height: auto;">
    <a-col class="brand-name">
      <a-icon type="infinity" class="mr-2" />
      <span class="brand-title">Projeto Chameleon</span>
    </a-col>
    <a-col>
      <CreateIssueModal v-model="dialog">ADD TASK</CreateIssueModal>
    </a-col>
  </a-row>
</template>

<script setup>
import { ref } from 'vue'
import CreateIssueModal from './modals/CreateIssueModal.vue'

const dialog = ref(false)
</script>

<style scoped>
.brand-name {
  display: flex;
  align-items: center;
}

.brand-title {
  font-size: larger;
  font-weight: bold;
}

.create-issue-btn {
  margin-left: 10px;
}
</style>
