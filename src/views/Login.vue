<template>
  <div class="container">
    <div class="row my-5">
      <div class="col-md-6 mx-auto">
        <h2>Login Page!</h2>

        <p v-if="auth=='fail'" class="text-danger">{{errMsg}}</p>

        <form v-on:submit.prevent="Login">
          <div class="form-group text-left">
            <label for="exampleInputEmail1">Email address</label>
            <input type="email" class="form-control" id="exampleInputEmail1" v-model="email">
          </div>
          <div class="form-group text-left">
            <label for="exampleInputPassword1">Password</label>
            <input type="password" class="form-control" id="exampleInputPassword1" v-model="password">
          </div>
          <div class="form-group form-check text-left">
            <input type="checkbox" class="form-check-input" id="exampleCheck1">
            <label class="form-check-label" for="exampleCheck1">Check me out</label>
          </div>
          <button type="submit" class="btn btn-primary">Login</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  //import ItemService from '@/services/ItemService.js'

  export default{
    data(){
      return {
        email: '',
        password: '',
        errMsg: ''
      }
    },
    methods:{
      Login(){
        let user = {username: this.email, password: this.password}
        this.$store.dispatch('login',user)
          .then(() => this.$router.push('/orders'))
          .catch(err => {
              console.log('There was an error:',err.response)
              this.errMsg = 'Login Failed!, Incorrect Email and Password'
            });
      }
    },
    computed:{
      auth(){
        return this.$store.getters.authStatus
      }
    }
  }
</script>

<style type="text/css">
  
</style>