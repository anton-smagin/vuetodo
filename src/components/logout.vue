<template>
  <div>
    <button class="btn" v-on:click="logout">
      Logout
    </button>
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
      logout () {
        localStorage.removeItem('token')
        this.$parent.loggedIn = false
      }
    }
  }
</script>
