<template>
  <a-layout id="inspire">
    <a-layout-header style="display: flex; text-align: center; justify-content: space-between; align-items: center;">
      <!-- Logo space -->
      <div class="header-logo">
        <a href="#">
          <img src="../assets/logo.png" alt="Logo" class="logo">
        </a>
      </div>
      <a-divider type="vertical" style="height: 50px; margin-left: 5px;"></a-divider>

      <!-- Search input -->
      <a-input-search
        placeholder="Pesquisar"
        style="max-width: 300px; margin: auto;"
        enter-button
      />

      <!-- Notifications and avatar space -->
      <div style="display: flex; align-items: center;">
        <a-dropdown>
          <a-menu slot="overlay">
            <a-menu-item key="1">
              <a-avatar style="background-color: blue; margin-right: 10px;">
                <span class="text-h5">IS</span>
              </a-avatar>
              <a-divider />
              <a-button type="link" block>
                Editar Conta
              </a-button>
              <a-divider />
              <a-button type="link" block>
                <router-link to="/">Desconectar</router-link>
              </a-button>
            </a-menu-item>
          </a-menu>
          <a-avatar style="background-color: blue; cursor: pointer;">
            <span class="text-h5">IS</span>
          </a-avatar>
        </a-dropdown>
        <div class="user-details">
          <b>Nome usuário</b>
          <p class="text-caption mt-1">Email usuário</p>
        </div>
      </div>
    </a-layout-header>

    <!-- Main content -->
    <a-layout-content>
      <BoardNav />
      <a-divider />
      <Board />
    </a-layout-content>
  </a-layout>
</template>

<script>
import Board from '../components/project/Board.vue'
import BoardNav from '../components/project/BoardNav.vue'
// import { mapState } from 'vuex'

export default {
  components: { Board, BoardNav },
  // computed: {
  //   ...mapState(['user']),
  //   userState() {
  //     return this.user
  //   },
  //   userInitials() {
  //     if (this.user && this.user.name) {
  //       const nameParts = this.user.name.split(' ')

  //       const firstNameInitial = nameParts[0].charAt(0)
  //       const lastNameInitial = nameParts.length > 1 ? nameParts[1].charAt(0) : ''

  //       return firstNameInitial.toUpperCase() + (lastNameInitial.toUpperCase() ? lastNameInitial.toUpperCase() : '')
  //     } else {
  //       return '';
  //     }
  //   }
  // },
  // created() {
  //   const storedUser = sessionStorage.getItem('user')
  //   const storedToken = sessionStorage.getItem('token')

  //   if (storedUser && storedToken) {
  //     this.$store.commit('setUser', JSON.parse(storedUser))
  //     this.$store.commit('setToken', storedToken)
  //   }
  // }
}
</script>

<style scoped>
.header-logo {
  margin: 0px 15px 0px 10px;
}

.logo {
  width: 40px;
  height: 40px;
}

.user-details {
  display: flex;
  flex-direction: column;
  margin-left: 10px;
  padding: 5px;
  text-align: left;
}

.ant-divider-vertical {
  height: 50px;
}
</style>
