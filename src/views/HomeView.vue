<template>
  <div class="common-layout">
    <a-layout>
      <a-layout-header class="header">
        <div class="header-left">
          <div class="header-logo">
            <img src="../assets/logo.png" alt="Logo" class="logo">
          </div>
          <a-divider type="vertical" style="margin-left: 5px;" />
        </div>
        <div class="header-center">
          <a-input-search placeholder="Pesquisar" v-model:value="searchQuery" class="search-input" />
        </div>
        <div class="header-right">
          <a-dropdown>
            <a-avatar size="large">
              <span class="text-h5">{{ userInitials }}</span>
            </a-avatar>
            <template #overlay>
              <a-menu>
                <a-menu-item key="logout">
                  <a-button type="text" @click="handleLogout">
                    Desconectar
                  </a-button>
                </a-menu-item>
              </a-menu>
            </template>
          </a-dropdown>
        </div>
        <div class="user-details">
          <b class="user-name">{{ userState.name }}</b>
          <span class="user-email">{{ userState.email }}</span>
        </div>
      </a-layout-header>
      <a-layout-content class="main">
        <BoardNav />
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
  methods: {
    handleLogout() {
      this.$store.dispatch('logoutUser')
      sessionStorage.clear()
      this.$router.push('/')
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
  justify-content: space-between;
  background-color: #f0f0f0;
  color: #000;
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
  align-items: center; /* Garante que o conteúdo esteja alinhado verticalmente */
}


.header-logo {
  margin: 15px 10px 15px -15px;
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
  justify-content: center;
  margin-left: 10px;
  padding: 10px 0px 10px 10px;
  text-align: left;
  color: black;
}

.user-name {
  font-weight: bold;
  margin-bottom: 2px;
  margin: 5px 0px -40px 0px;
}

.user-email {
  font-size: 14px;
}
</style>
