<template>
  <div>
    <input placeholder="login" type="email" v-model="email">
    <input placeholder="password" type="password" v-model="password">
    <button class="btn" v-on:click="login">Login</button>
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
