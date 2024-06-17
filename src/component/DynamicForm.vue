<template>
  <div
    class="user-form-container bg-gray-100 rounded-lg shadow-lg p-8 max-w-xl mx-auto mt-8"
  >
    <h1 class="text-3xl font-bold text-center mb-8">Formulário Dinâmico</h1>
    <form @submit.prevent="handleSubmit">
      <div class="user-form mb-4 p-4 bg-white rounded-lg shadow-md">
        <div class="mb-4">
          <label for="name" class="block text-gray-700">Nome:</label>
          <input
            v-model="newUser.name"
            type="text"
            class="form-input mt-1 block w-full rounded-lg p-2"
            placeholder="Nome"
            required
          />
        </div>
        <div class="mb-4">
          <label for="email" class="block text-gray-700">Email:</label>
          <input
            v-model="newUser.email"
            type="email"
            class="form-input mt-1 block w-full rounded-lg p-2"
            placeholder="Email"
            required
          />
        </div>
        <div class="mb-4">
          <label for="phone" class="block text-gray-700">Telefone:</label>
          <input
            v-model="newUser.phone"
            type="tel"
            class="form-input mt-1 block w-full rounded-lg p-2"
            placeholder="Telefone"
            required
          />
        </div>
        <button
          type="button"
          @click="addUser"
          class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded-lg"
        >
          Adicionar Usuário
        </button>
      </div>
      <button
        type="submit"
        class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-lg"
      >
        Enviar
      </button>
    </form>

    <div v-if="users.length > 0" class="mt-8">
      <h2 class="text-2xl font-bold mb-4">Usuários Cadastrados:</h2>
      <ul class="divide-y divide-gray-200">
        <li v-for="(user, index) in users" :key="index" class="py-2">
          <div class="flex items-center">
            <div class="flex-1">
              <span class="blocktext-lg">{{ `Nome: ${user.name}` }}</span>
              <span class="block text-gray-600">{{
                `Email: ${user.email}`
              }}</span>
              <span class="block text-gray-600">{{
                `Telefone: ${user.phone}`
              }}</span>
            </div>
            <button
              @click="removeUser(index)"
              class="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded-lg"
            >
              Remover
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Dados do formulário
      newUser: { name: "", email: "", phone: "" },
      // Lista de usuários
      users: [],
    };
  },
  methods: {
    addUser() {
      if (this.newUser.name && this.newUser.email && this.newUser.phone) {
        this.users.push(this.newUser);
        this.newUser = { name: "", email: "", phone: "" };
      }
    },

    removeUser(index) {
      this.users.splice(index, 1);
    },

    handleSubmit() {
      localStorage.setItem("users", JSON.stringify(this.users));
      alert("Formulário enviado com sucesso!");
    },
  },
};
</script>

<style>
.user-form-container {
  margin-top: 50px;
  margin-bottom: 50px;
}

.user-form {
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.btn {
  margin-right: 10px;
}
</style>
