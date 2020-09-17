<template>
  <div class="container">
    <div class="row my-5">
      <div class="col-md-6 mx-auto">
        <h2>Register Page!</h2>
        <form>
          <div class="form-group text-left">
            <label for="exampleInputName">Name</label>
            <input type="text" class="form-control" id="exampleInputName">
          </div>
          <div class="form-group text-left">
            <label for="exampleInputEmail1">Email address</label>
            <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"  v-model="email">
            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
          </div>
          <div class="form-group text-left">
            <label for="exampleInputPassword1">Password</label>
            <input type="password" class="form-control" id="exampleInputPassword1">
          </div>
          <div class="form-group text-left">
            <label for="exampleInputConfirmPassword">Confirm Password</label>
            <input type="password" class="form-control" id="exampleInputConfirmPassword">
          </div>
          <button type="submit" class="btn btn-primary btn-block">Create</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
 import ItemService from '@/services/ItemService.js'
  export default{
    data(){
      return {
        name:null,
        email:null,
        password:null,
        confirmpassword:null,
        errorPasswordMessage:false,
        Active:true
      };
    },
    watch:{
      confirmpassword(value){
        this.confirmpassword=value
        this.matchPassword(value);
      }
    },
    methods:{
      matchPassword(value){
        if (this.password && value && (this.password !== value)) {
          this.errorPasswordMessage=true;
          
        }else{
          this.errorPasswordMessage = false;
          this.Active=false;
        }
      },
      register(){
        let user={name:this.name,email:this.email,password:this.password};
        ItemService.register(user).
        then(()=>{
          this.$router.push('/login')
        }).catch(err=>{
          if (err.response.status) {
            this.errorMessage = err.response.data.errors
          }
        })
      }
    }
  }
</script>

<style type="text/css">
  
</style>