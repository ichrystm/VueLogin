<template> 

  <div>
    <br>
    <h1>Edição de Usuário</h1>
    <hr>
    <div class="columns is-centered">
      <div class="column is-half">
          <div v-if="error != undefined">
            <div class="notification is-danger">
              <p>{{error.nome}}</p>
              <p>{{error.email}}</p>
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
          <button class="button is-success" @click="update()">Editar</button>
      </div>
    </div>

  </div>
  
</template>

<script>
import axios from 'axios';
export default {

  created(){

    var req = {
        headers: {
        Authorization: 'Bearer ' + localStorage.getItem('token')
        }
      }

    axios.get("http://localhost:8686/user/" + this.$route.params.id, req)
    .then(res => {
      console.log(res.data[0])
      this.name = res.data[0].name;
      this.email = res.data[0].email;
      this.id = res.data[0].id;
    })
    .catch(err => {
      console.log(err);
      this.$router.push({name: 'Users'});
    })

  },

  data(){
    return {
      name: '',
      email: '',
      id: -1,
      error: undefined,
    }
  },
  methods: {
    update(){
      
      var req = {
        headers: {
        Authorization: 'Bearer ' + localStorage.getItem('token')
        }
      }

      axios.put("http://localhost:8686/user", {
        name: this.name,
        email: this.email,
        id: this.id
      }, req).then(res => {
        console.log(res);
        this.$router.push({name: 'Users'});
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