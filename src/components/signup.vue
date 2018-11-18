<template>
  <div>
    <input placeholder="login" type="email" v-model="email">
    <input placeholder="password" type="password" v-model="password">
    <button class="btn" v-on:click="signup">Sign Up</button>
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
      signup () {
        let vue = this
        axios
          .post('https://gttodo.herokuapp.com/signup', {
            email: this.email,
            password: this.password,
          })
          .then(function() {
            vue.$parent.login = true
          })
          .catch(function(data) {
            /* eslint-disable */
            return console.log(data)
          })
    }
  }
}
</script>
