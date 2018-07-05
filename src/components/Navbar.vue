<template>
    <div>
    <v-toolbar
      absolute
      color="black"
      dark
    > 
      <v-toolbar-title class="warna"> <v-btn @click="backHome" flat>BLOG</v-btn> </v-toolbar-title>

      <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down" >
      <v-btn flat v-if="loginStatus == true" to="/upload" >
        <v-icon >cloud_upload</v-icon>
        upload
      </v-btn>
      <v-btn flat v-if="loginStatus == true" @click="logout">
        logout
      </v-btn>

      <v-btn to="login" flat v-if="loginStatus==false"> Login
      </v-btn>
      <v-btn to="register" flat v-if="loginStatus==false"> Register
      </v-btn>
    </v-toolbar-items>
    </v-toolbar>
    </div>
</template>
<script>
import swal from 'sweetalert'
export default{
  methods: {
    backHome () {
      window.location('/')
    },
    logout () {
      console.log('clear consolelog')
      swal({
        title: "Are you sure to logout?",
        text: "Once logout, you need to login again!",
        icon: "warning",
        buttons: true,
        dangerMode: true,
      })
      .then((willDelete) => {
        if (willDelete) {
          swal('You already logout', {
            icon: "success",
          });
          localStorage.clear()
          window.location = '/'
        } 
        else {
          swal("You gak jadi logout");
        }
      });
    }
  },
  data () {
    return {
      dialog: false,
      loginStatus: false
    }
  },
  created () {
    if (localStorage.hasOwnProperty('token')) {
      this.loginStatus = true
    }
    else{
      this.loginStatus = false
    }
  }
}
</script>

<style lang="scss" scoped>
  .cont {
    background-color: #CFD8DC
  }
  .warna {
      text-decoration-color: #CFD8DC
  }
</style>


