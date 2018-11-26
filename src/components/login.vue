<template>
  <div>
    <div class="row">
      <div class="col12 text-center">
        <div class="input-group">
          <input id="new-login" type="email" placeholder="Email" v-model="email">
          <input id="new-password" type="password" placeholder="Password" v-model="password">
          <button id="log-in" class="btn" v-on:click="login">Log In</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data () {
      return {
        email: '',
        password: '',
      }
    },
    methods: {
      login () {
        let vue = this
        axios
          .post('https://gttodo.herokuapp.com/login', {
            email: this.email,
            password: this.password,
          })
          .then(function(response) {
            localStorage.setItem('token', response.data.token)
            vue.$parent.loggedIn = true
          })
          .catch(function(data) {
            /* eslint-disable */
            return console.log(data)
          })
      }
    }
  }
</script>
