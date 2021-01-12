<template> 

  <div>
    <br>
    <h1>Registro de Usuário</h1>
    <hr>
    <div class="columns is-centered">
      <div class="column is-half">
          <div v-if="error != undefined">
            <div class="notification is-danger">
              <p>{{error.nome}}</p>
              <p>{{error.email}}</p>
              <p>{{error.senha}}</p>
              <p>{{error.error}}</p>
            </div>
          </div>
          <br>
          <p>Nome:</p>
          <input type="text" placeholder="Nome" class="input" v-model="name">
          <br>
          <br>
          <p>E-mail:</p>
          <input type="text" placeholder="E-mail" class="input" v-model="email">
          <br>
          <br>
          <p>Senha:</p>
          <input type="password" placeholder="*******" class="input" v-model="password">
          <br>
          <br>
          <button class="button is-success" @click="register">Cadastrar</button>
      </div>
    </div>

  </div>
  
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return {
      name: '',
      password: '',
      email: '',
      error: undefined,
    }
  },
  methods: {
    register(){
      axios.post("http://localhost:8686/user", {
        name: this.name,
        email: this.email,
        password: this.password,
      }).then(res => {
        console.log(res);
        this.$router.push({name: 'Home'});
      })
      .catch(err => {
        var msgError = err.response.data;
        this.error = msgError;
        console.log(msgError.error)
      })
    }
  }
}
</script>

<style scoped>

</style>