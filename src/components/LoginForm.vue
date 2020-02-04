<template>
  <form class="form-login">
    <label>CPF:</label>
    <input type="text" v-model="credentials.cpf" placeholder="Digite seu CPF aqui" />
    <label>Conta:</label>
    <input
      type="text"
      v-model="credentials.account"
      placeholder="Digite os 4 ultimos do cartão aqui"
    />
    <label>Senha:</label>
    <input
      type="password"
      v-model="credentials.password"
      placeholder="Digite sua senha de 4 digitos aqui"
    />
    <button @click="login(credentials)">Logar!</button>
  </form>
</template>

<script>
import axios from 'axios'
const client = axios.create({
  baseURL: 'https://localhost:8001/'
})

export default {
  name: 'LoginForm',
  data: () => {
    return {
      credentials: {
        cpf: '',
        account: '',
        password: ''
      },
      response: {}
    }
  },
  methods: {
    login: credentials => {
      const { cpf, account, password } = credentials
      client.post(`/user-info?cpf=${cpf}&account=${account}&password=${password}`).then((res) => {
        console.log(res)
        this.response = res
      })
    }
  }
}
</script>

<style scoped>
* {
  font-family: monospace;
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
}
.form-login {
  width: 450px;
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 15px;
  margin: 0 auto;
}
.form-login label {
  display: block;
  margin-bottom: 5px;
  font-size: 15px;
}
.form-login input,
.form-login button {
  width: 100%;
  display: block;
  padding: 15px;
  font-size: 15px;
  border-radius: 3px;
  outline: none;
}
.form-login button {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
  font-weight: bold;
  border: none;
}
.form-login button:focus {
  color: #fff;
  background-color: #0069d9;
  border-color: #0062cc;
  box-shadow: 0 0 0 0.2rem rgba(38, 143, 255, 0.5);
}
.form-login button:hover {
  color: #fff;
  background-color: #0069d9;
  border-color: #0062cc;
}

.form-login input {
  margin-bottom: 10px;
  border: 1px solid #ccc;
}

.form-login input:focus {
  border: 2px solid #0c5460;
}
</style>
