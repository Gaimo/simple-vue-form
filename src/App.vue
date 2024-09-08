<script setup>
import { ref } from 'vue'
import CustomInput from './components/CustomInput.vue'

// Referências para os campos de entrada
const username = ref('')
const password = ref('')
const repassword = ref('')

// Função para criar a conta
const createAccount = () => {
  console.log('Username: ', username.value)
  console.log('Password: ', password.value)
  console.log('Repassword: ', repassword.value)
}

</script>

<template>
  <div>
    <!-- Form -->
    <div class="form">
      <h2>Sign Up</h2>

      <div class="form-element">
        <label for="username">
          Username:
        </label>
        <CustomInput v-model="username" id="username" type="text" placeholder="Enter your username"/>
      </div>

      <div class="form-element">
        <label for="password">
          Password:
        </label>
        <CustomInput v-model="password" id="password" type="password" placeholder="Enter your password"/>
      </div>

      <div class="form-element">
        <label for="repassword">
          Repeat the password:
        </label>
        <CustomInput v-model="repassword" id="repassword" type="password" placeholder="Repeat the password"/>
      </div>

      <button @click="createAccount">Register</button>

    </div>
  </div>
</template>

<style scoped>
.form {
  border: 1px solid white;
  width: 500px;
  padding-bottom: 32px;
  border-radius: 8px;
}

.form-element {
  display: flex;
  flex-direction: column;
  gap: 8px;
  max-width: 300px;
  margin: 16px auto 0 auto;
}

.form-element {
  label {
    text-align: left;
  }
}

button {
  margin-top: 32px;
  width: 300px;
}


</style>
