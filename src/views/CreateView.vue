<template>
  <div class="container">
    <a-card class="mx-auto pa-12 pb-8">
      <div class="header-logo center-card">
        <img src="../assets/logo.png" alt="Logo" class="logo" />
      </div>

      <a-form layout="vertical" :model="form" style="min-width:400px; max-width: 600px; display: flex; flex-direction: column">
        <a-form-item label="Nome">
          <a-input v-model:value="form.name" placeholder="Nome & Sobrenome" allow-clear />
        </a-form-item>
        <a-form-item label="Email">
          <a-input v-model:value="form.email" placeholder="seumail@exemplo.com" allow-clear />
        </a-form-item>
        <a-form-item label="Senha">
          <a-input-password v-model:value="form.password" placeholder="Insira sua senha" allow-clear />
        </a-form-item>

        <a-form-item>
          <div class="avatar-form-item">
            <a-avatar size="large">
              <a-button shape="circle" :size="small" type="primary">
                <CameraTwoTone/>
                <input type="file" ref="fileInput" class="file-input" @change="handleFileUpload" />
              </a-button>
            </a-avatar>
          </div>
        </a-form-item>

        <a-button @click="submitForm" type="primary" size="large" block>
          <router-link to="/" class="text-white">
            <b>Criar novo usuário</b>
          </router-link>
        </a-button>
      </a-form>

      <div class="router-button">
        <router-link to="/" class="text-blue">
          Voltar <a-icon type="arrow-right" />
        </router-link>
      </div>
    </a-card>
  </div>
</template>

<script>
import { CameraTwoTone } from '@ant-design/icons-vue'

export default {
  components: {
    CameraTwoTone
  },
  data() {
    return {
      form: {
        name: '',
        email: '',
        password: '',
      },
      visible: false,
    };
  },
  methods: {
    async submitForm() {
      try {
        await this.$store.dispatch('createUserStore', { userForm: this.form });
        return true;
      } catch (error) {
        throw error;
      }
    },
    handleFileUpload() {
      const file = this.$refs.fileInput.files[0];
      console.log('Arquivo selecionado:', file);
    },
  },
};
</script>

<style scoped>
.text-white{
  text-decoration: none;
}

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
  text-decoration: none;
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

.avatar-form-item {
  display: flex;
  justify-content: center;
}

.file-input {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
}
</style>
