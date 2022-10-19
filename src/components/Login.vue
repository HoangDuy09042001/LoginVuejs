<template>
  <section class="vh-100">
      <div class="container py-5 h-100">
        <div class="row d-flex align-items-center justify-content-center h-100">
          <div class="col-md-8 col-lg-7 col-xl-6">
            <img
              src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.svg"
              class="img-fluid"
              alt="Phone image"
            />
          </div>
          <div class="col-md-7 col-lg-5 col-xl-5 offset-xl-1">
            <form>
              <!-- Email input -->
              <div class="form-outline mb-4">
                <input
                  type="email"
                  id="form1Example13"
                  class="form-control form-control-lg"
                  v-model="email"
                />
                <label class="form-label" for="form1Example13"
                  >Email address</label
                >
              </div>

              <!-- Password input -->
              <div class="form-outline mb-4">
                <input
                  type="password"
                  id="form1Example23"
                  class="form-control form-control-lg"
                  v-model="password"
                />
                <label class="form-label" for="form1Example23">Password</label>
              </div>

              

              <!-- Submit button -->
              <button @click.prevent="login" type="submit" class="btn btn-primary btn-lg btn-block">
                Sign in
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
</template>

<script>
import axios from "axios";
export default {
  name: 'LoginForm',
  data(){
    return {
        email: '',
        password: '',
    }
  },
  methods: {
    async login(){
        //Email: Sincere@april.biz
        //Password: Bret
        let result = await axios.get(
            `https://jsonplaceholder.typicode.com/users?email=${this.email}&username=${this.password}`
        )
        if(result.status == 200 && result.data.length >0){
            localStorage.setItem("user-info", JSON.stringify(result.data[0]));
            alert('You have successfully logged in');
        }
        console.log(result);
    }
  },
  mounted(){
    let user = localStorage.getItem('user-info');
    if(user){
        alert('Mounted');
    }
  }
}
</script>

<style>
@import "~bootstrap/dist/css/bootstrap.css";
.divider:after,
.divider:before {
  content: "";
  flex: 1;
  height: 1px;
  background: #eee;
}
</style>