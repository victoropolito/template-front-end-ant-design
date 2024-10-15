<template>
  <a-row justify="space-between" class="custom-row">
    <a-col :span="12" class="left-align">
      <div class="brand-title"><strong>Projeto Chameleon</strong></div>
    </a-col>
    <a-col :span="12" class="right-align">
      <create-issue-modal/>
    </a-col>
  </a-row>
</template>

<script setup>
import createIssueModal from './modals/CreateIssueModal.vue'
</script>

<style scoped>
.custom-row {
  width: 100%;
  padding: 15px 25px 0px 25px;
}

.left-align {
  text-align: left;
}

.right-align {
  text-align: right;
}

.board-nav {
  margin-bottom: 20px;
  max-height: 300px;
  overflow: auto;
  display: flex;
  justify-content: space-between;
}

.brand-title {
  font-size: larger;
  display: flex;
  align-items: center;
  color: black;
}
</style>
