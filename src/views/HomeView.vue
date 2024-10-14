<template>
  <div class="common-layout">
    <a-layout style="padding-top: 5px">
      <a-layout-header class="header">
        <div class="header-left">
          <!-- Logo space -->
          <div class="header-logo">
            <!-- <img src="@/assets/logo.png" alt="Logo" class="logo"> -->
          </div>

          <!-- Divider -->
          <a-divider type="vertical" style="margin-left: 5px;" />
        </div>

        <!-- Search input -->
        <div class="header-center">
          <a-input-search placeholder="Pesquisar" v-model:value="searchQuery" class="search-input" />
        </div>

        <!-- Notifications and avatar space -->
        <div class="header-right">
          <a-dropdown>
            <a-avatar size="large">
              <span class="text-h5">{{ userInitials }}</span>
            </a-avatar>
            <template #overlay>
              <a-menu>
                <a-menu-item key="edit">
                  <a-button type="text">Editar Conta</a-button>
                </a-menu-item>
                <a-menu-item key="logout">
                  <a-button type="text">
                    <router-link to="/">Desconectar</router-link>
                  </a-button>
                </a-menu-item>
              </a-menu>
            </template>
          </a-dropdown>

          <div class="user-details">
            <b class="user-name">{{ userState.name }}</b>
            <p class="text-caption mt-1">{{ userState.email }}</p>
          </div>
        </div>
      </a-layout-header>

      <!-- Main content -->
      <a-layout-content class="main">
        <BoardNav class="board-nav" />
        <a-divider />
        <Board :userId="userState.id" />
      </a-layout-content>
    </a-layout>
  </div>
</template>

<script>
import Board from '../components/project/Board.vue'
import BoardNav from '../components/project/BoardNav.vue'
import { mapState } from 'vuex'

export default {
  components: { Board, BoardNav },
  data() {
    return {
      searchQuery: ''
    }
  },
  computed: {
    ...mapState(['user']),
    userState() {
      return this.user
    },
    userInitials() {
      if (this.user && this.user.name) {
        const nameParts = this.user.name.split(' ')
        const firstNameInitial = nameParts[0].charAt(0)
        const lastNameInitial = nameParts.length > 1 ? nameParts[1].charAt(0) : ''
        return firstNameInitial.toUpperCase() + (lastNameInitial.toUpperCase() ? lastNameInitial.toUpperCase() : '')
      } else {
        return ''
      }
    }
  },
  created() {
    const storedUser = sessionStorage.getItem('user')
    const storedToken = sessionStorage.getItem('token')

    if (storedUser && storedToken) {
      this.$store.commit('setUser', JSON.parse(storedUser))
      this.$store.commit('setToken', storedToken)
    }
  }
}
</script>

<style scoped>
.a-layout {
  display: flex;
  flex-direction: column;
}

.a-layout-content {
  height: 100vh;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between; /* Espaço entre os elementos principais */
}

.header-left,
.header-center,
.header-right {
  display: flex;
  align-items: center;
}

.header-left {
  flex: 1;
  justify-content: flex-start;
}

.header-center {
  flex: 1;
  justify-content: center;
}

.header-right {
  flex: 1;
  justify-content: flex-end;
}

.header-logo {
  margin: 0px 15px 0px 10px;
}

.logo {
  width: 40px;
  height: 40px;
}

.search-input {
  max-width: 500px;
  width: 100%;
}

.user-details {
  display: flex;
  flex-direction: column;
  margin-left: 10px;
  padding: 5px;
  text-align: left;
  color: black;
}

.user-name {
  font-weight: bold;
}
</style>
