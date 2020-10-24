<template>
    <div class="container-fluid">
      <b-row class="card home">
        <b-col lg="12">
          <b-row>
            <b-col lg="6" class="image">
              <div class="left ">
                <img src="../assets/img/foodcourt-logo.png">
              </div>
            </b-col>
            <b-col lg="6" cols="12" class="card-body my-5">
              <div class="right ">
                <b-row>
                  <b-col lg="12" class="text-center">
                    <h2 class="mt-3" v-warna="red">Login</h2>
                  </b-col>
                  <b-col lg="12" cols="12">
                    <form v-on:submit.prevent="onLogin()">
                      <div class="form-group">
                        <input v-model="form.email" placeholder="Email" type="email" class="form-control">
                      </div>
                      <div class="form-group">
                        <input v-model="form.password" placeholder="Password" type="password" class="form-control">
                      </div>
                      <b-col lg="12">
                        <b-row>
                          <b-col lg="4" cols="4">
                            <button type="submit" class="btn btnStyle">Login</button>
                          </b-col>
                          <b-col lg="8" cols="8">
                            <b-col lg="12" cols="12" class="register">Don't have account? <router-link class="linkStyle" to="/register">Sign up</router-link></b-col>
                          </b-col>
                        </b-row>
                      </b-col>
                    </form>
                  </b-col>
                </b-row>
              </div>
            </b-col>
          </b-row>
        </b-col>
      </b-row>
    </div>
</template>
<script>
import Swal from 'sweetalert2'
import { mapActions } from 'vuex'
export default {
  title: 'Foodcourt | Login',
  data () {
    return {
      form: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    onLogin () {
      if (this.form.email === '' || this.form.password === '') {
        Swal.fire({
          icon: 'error',
          title: 'Cannot be empty!'
        })
      } else {
        this.actionLogin(this.form)
          .then((response) => {
            if (response === 'Login Success') {
              window.location = '/'
            } else {
              Swal.fire({
                icon: 'error',
                title: 'Oops...',
                text: `${response}`
              })
            }
          })
          .catch(() => {
            Swal.fire({
              icon: 'error',
              title: 'Oops...',
              text: 'Something went wrong!'
            })
          })
      }
    },
    ...mapActions({
      actionLogin: 'auth/login'
    })
  }
}
</script>
<style scoped>
.linkStyle {
  text-decoration: none;
  color: #04b4bc;
}
.btnStyle{
  width: 100%;
  background: #04b4bc;
  color: #fff;
}
.btnStyle:hover{
  background: #fff;
  border-color: #04b4bc;
  color: #04b4bc;
}
.left img{
  width: 70%;
}
.home{
  margin: 50px;
}

@media only screen and (max-width: 500px) {
  .image {
    display: none;
  }
  .home{
  margin: 0px;
}
.register{
  font-size: 11px;
}
}
</style>
