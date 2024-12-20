<template>
    <div class="px-4 sm:px-6 lg:px-8">
        <div class="sm:flex sm:items-center">
            <div class="sm:flex-auto">
                <h1 class="text-xl font-semibold text-gray-900">Criar Novo Usuário</h1>
                <p class="mt-2 text-sm text-gray-700">Preencha as informações abaixo para cadastrar um novo usuário no
                    sistema.</p>
            </div>
        </div>
        <div class="mt-8 flex flex-col">
            <div class="shadow ring-1 ring-black ring-opacity-5 md:rounded-lg bg-white p-6">
                <form @submit.prevent="handleSubmit">
                    <!-- Nome -->
                    <div class="mb-4">
                        <label for="name" class="block text-sm font-medium text-gray-700">Nome</label>
                        <input type="text" id="name" v-model="form.name"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                    </div>
                    <!-- E-mail -->
                    <div class="mb-4">
                        <label for="email" class="block text-sm font-medium text-gray-700">E-mail</label>
                        <input type="email" id="email" v-model="form.email"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                    </div>
                    <!-- Telefone -->
                    <div class="mb-4">
                        <label for="phone" class="block text-sm font-medium text-gray-700">Telefone</label>
                        <input type="text" id="phone" v-model="form.phone"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                    </div>
                    <!-- Data de Cadastro -->
                    <div class="mb-4">
                        <label for="created_at" class="block text-sm font-medium text-gray-700">Data de Cadastro</label>
                        <input type="date" id="created_at" v-model="form.created_at"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                    </div>
                    <!-- Senha -->
                    <div class="mb-4">
                        <label for="password" class="block text-sm font-medium text-gray-700">Senha</label>
                        <input type="password" id="password" v-model="form.password"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                    </div>
                    <!-- Botão de Salvar -->
                    <div class="mt-6 text-right">
                        <button type="submit"
                            class="inline-flex items-center justify-center rounded-md border border-transparent bg-indigo-600 px-4 py-2 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                            Salvar Usuário
                        </button>
                    </div>
                </form>
            </div>
        </div>
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
                created_at: '',
                password: '',
            },
        };
    },
    methods: {
        async handleSubmit() {
            try {
                if (this.form.created_at) {
                    const date = new Date(this.form.created_at);
                    this.form.created_at = date.toISOString().split('T')[0];
                }
                
                await axios.post('http://127.0.0.1:8000/api/users', this.form);
                alert('Usuário salvo com sucesso!');
                this.$router.push('/users'); // Redireciona para a lista de usuários
            } catch (error) {
                console.error('Erro ao salvar usuário:', error);
                alert('Erro ao salvar o usuário. Por favor, tente novamente.');
            }
        },
    },
};
</script>