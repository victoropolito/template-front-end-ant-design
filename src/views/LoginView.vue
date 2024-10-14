<template>
  <div class="container">
    <a-card
      class="mx-auto pa-12 pb-8"
      hoverable
    >
      <div class="header-logo center-card">
        <!-- <img src="@/assets/logo.png" alt="Logo" class="logo" /> -->
        <!-- <Image
        width={200}
        src="https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png"
        /> -->
      </div>

      <a-form
        layout="vertical"
        :model="form"
        style="min-width:400px; max-width: 600px; display: flex; flex-direction: column"
      >
        <a-form-item label="Email">
          <a-input
            v-model:value="form.email"
            placeholder="seumail@exemplo.com"
            allow-clear
          />
        </a-form-item>
        <a-form-item label="Senha">
          <a-input-password
            v-model:value="form.password"
            placeholder="Insira sua senha"
            allow-clear
            :visibilityToggle="true"
          />
        </a-form-item>
        <a-alert
          v-if="showError"
          message="Erro ao fazer login. Verifique suas credenciais."
          type="error"
          show-icon
          class="mb-12"
        />
  
        <a-button
          :disabled="!validForm"
          type="primary"
          size="large"
          block
          @click="handleLogin"
        >
          Acessar
        </a-button>
      </a-form>

      <div class="router-button">
        <router-link to="/create" class="text-blue">
          Cadastrar agora
        </router-link>
      </div>
    </a-card>
  </div>
</template>

<script>
// import { Image } from 'antd'

export default {
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
      showError: false,
    }
  },
  computed: {
    validForm() {
      return this.form.email && this.form.password;
    },
  },
  methods: {
    async handleLogin() {
      try {
        await this.$store.dispatch('createUserSessionStore', { userForm: this.form });
        this.showError = false;
        this.$router.push('/home');
      } catch (error) {
        console.error('Error during login:', error);
        this.showError = true;
      }
    },
  },
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}

.router-button {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 5px 0 0 0;
  font-size: small;
}

.text-blue {
  color: rgb(8, 73, 158);
}

.header-logo {
  margin-bottom: 20px;
}

.logo {
  width: 150px;
  height: 150px;
}

.center-card {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
