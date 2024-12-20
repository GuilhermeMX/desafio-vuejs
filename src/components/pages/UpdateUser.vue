<template>
    <div>
      <h1>Atualizar Usuário</h1>
      <form @submit.prevent="updateUser">
        <label for="name">Nome</label>
        <input v-model="form.name" type="text" id="name" required />
  
        <label for="email">Email</label>
        <input v-model="form.email" type="email" id="email" required />
  
        <label for="phone">Telefone</label>
        <input v-model="form.phone" type="text" id="phone" required />
  
        <label for="password">Senha</label>
        <input v-model="form.password" type="password" id="password" required />
  
        <button type="submit">Salvar</button>
      </form>
    </div>
</template>
  
<script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        form: {
          name: '',
          email: '',
          phone: '',
          password: '',
        },
      };
    },
    mounted() {
      this.fetchUserData();
    },
    methods: {
      async fetchUserData() {
        try {
          const response = await axios.get(`/api/users/${this.$route.params.id}`);
          this.form = response.data.data;
        } catch (error) {
          console.error('Erro ao carregar os dados do usuário:', error);
        }
      },
      async updateUser() {
        try {
          await axios.put(`/api/users/${this.$route.params.id}`, this.form);
          alert('Usuário atualizado com sucesso!');
        } catch (error) {
          console.error('Erro ao atualizar o usuário:', error);
        }
      },
    },
  };
</script>
  