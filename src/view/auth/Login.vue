<template>
  <div>
    <div class="container">
      <h1>Auth State: {{ authState }}</h1>
      <form>
        <div class="form-group">
          <label for="email">Email address</label>
          <input
            type="email"
            name="email"
            v-model="email"
            class="form-control"
            id="email"
            aria-describedby="emailHelp"
            placeholder="Enter email"
          />
        </div>
        <div class="form-group">
          <label for="password">Password</label>
          <input
            type="password"
            name="password"
            v-model="password"
            class="form-control"
            id="password"
            placeholder="Password"
          />
        </div>

      </form>
      <button type="submit" @click="login" class="btn btn-primary">Logar</button>
      <button @click="setDeslogarAct" class="btn btn-danger">Deslogar</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ls from 'local-storage'
import { mapState, mapActions  } from 'vuex'

export default {
  data: () => ({
    msg: "Login",
    email: "",
    password: ""
  }),

  beforeCreate(){
    //console.log('beforeCreate')
    //this.$store.commit('initialiseStore');

    //Observa as alterações persistidas na tecla em outras guias. 
    //Dispara fn quando ocorre uma alteração, passando os seguintes argumentos.
    //ls.on(key, fn)
    // var _this = this
    // ls.on('statezera', function(val) {
    //   _this.callback()
    // })    
  },

  created() {
    // console.log('Logado', this.logado)
    // console.log('Logado', this.token)
    // console.log('STATE', this.$store.state.auth)
  },

  watch: {
    // authState: {
    //   handler: function(newValue, oldValue) {
    //     //console.log('oldValue: ', oldValue, typeof(oldValue), '  -  newValue: ', newValue, typeof(newValue))
    //     if(oldValue != newValue)
    //       console.log('DIFERENTE')
          
    //     ls.set('statezera', this.$store.state)
    //   },
    //   deep: true
    // },  
  },

  computed: {
    ... mapState('auth',{
      logado: 'logado',
      token: 'token'
    }),
    authState() {
      return this.$store.state.auth
    }
  },

  methods: {
    // callback () {
    //   //console.log('OLA callback INSIDE')
    //   this.$store.replaceState(ls.get('statezera'))
    //   //this.$store.state = ls.get('statezera');
    // },   
    
    ... mapActions('auth' ,{
      setLogarAct: 'setLogarAct',
      setDeslogarAct: 'setDeslogarAct',
    }),

    login() {

      axios({
        method: 'post',
        url: 'https://produto-b14ca.firebaseio.com/produtos.json',
        data: {
          email: 'hpeluzio@gmail.com',
          password: '123123'
        },
        // headers: {
        //   Authorization: "Bearer " + this.token
        // }        
      })
        .then(response => {
          if (response.data.token) {
            console.log(response.data)
          }
        })
        .catch(error => {
          console.log("Erro!");
          //this.errors.add({ field: 'auth', msg: 'E-mail ou senha inválidos' })
        });

      // axios({
      //   method: "post",
      //   url: URL + ":" + PORT + "/login",
      //   data: {
      //     email: this.email,
      //     password: this.password
      //   },
      //   headers: {
      //     Authorization: "Bearer " + this.token
      //   }        
      // })
      //   .then(response => {
      //     if (response.data.token) {
      //       //console.log(response.data)
      //       this.setLogarAct({ 
      //         logado: true, 
      //         token: response.data.token.token,
      //         name: response.data.user.name,
      //         email: response.data.user.email,
      //         permission: response.data.user.permission,
      //       })

      //       // this.setLogadoAct(true)
      //       // this.setTokenAct(response.data.token.token)
      //       // this.setNameAct(response.data.user.name)
      //       // this.setEmailAct(response.data.user.email)
      //       // this.setPermissionAct(response.data.user.permission)
      //       // Se entrar aqui autenticou com sucesso

      //       //alert('Logou!')
      //       //this.$router.push('/')
      //       //localStorage.setItem("user", JSON.stringify(response.data));
      //     }
      //   })
      //   .catch(error => {
      //     console.log("Erro!");
      //     //this.errors.add({ field: 'auth', msg: 'E-mail ou senha inválidos' })
      //   });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
