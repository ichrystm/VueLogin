<template> 

  <div>
    <br>
    <h1>Login</h1>
    <hr>
    <div class="columns is-centered">
      <div class="column is-half">
          <div v-if="error != undefined">
            <div class="notification is-danger">
              <p>{{error}}</p>
            </div>
          </div>
          <br>
          <p>E-mail:</p>
          <input type="text" placeholder="E-mail" class="input" v-model="email">
          <br>
          <br>
          <p>Senha:</p>
          <input type="password" placeholder="*******" class="input" v-model="password">
          <br>
          <br>
          <button class="button is-success" @click="login">Login</button>
      </div>
    </div>

  </div>
  
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return {
      password: '',
      email: '',
      error: undefined,
    }
  },
  methods: {
    login(){
      axios.post("http://localhost:8686/login", {
        email: this.email,
        password: this.password,
      }).then(res => {
        console.log(res);
        localStorage.setItem('token', res.data.token);
        this.$router.push({name: 'Home'});
      })
      .catch(err => {
        var msgError = err.response.data;
        this.error = msgError.error;
      })
    }
  }
}
</script>

<style scoped>

</style>