<template>
  <v-main class="appbackground application">
    <v-container grid-list-md  >
      <v-row align="center" justify="center">
        <v-col cols="12" sm="6" md="4" lg="4">
          <v-card class="mx-auto elevation-6" >

  <div class="vue-tempalte"  >
    <form>
      <h3 style="margin-left: 100px">Sign Up</h3>

      <div class="form-group" >
        <label style="margin-left: 10px">UserName</label>
        <input v-model="user.username" type="text" class="form-control form-control-lg" style="width: 300px;margin-left: 10px"/>
      </div>

      <div class="form-group">
        <label style="margin-left: 10px">Email address</label>
        <input v-model="user.email" type="email" class="form-control form-control-lg" style="width: 300px;margin-left: 10px" />
      </div>

      <div class="form-group">
        <label style="margin-left: 10px">Password</label>
        <input v-model="user.password" type="password" class="form-control form-control-lg" style="width: 300px;margin-left: 10px" />
      </div>

      <v-btn v-if="!isUpdate" class="green white--text" @click="saveUser" style="margin-top: 10px;margin-left: 10px">Sign Up</v-btn>

      <p class="forgot-password" style="margin-left: 10px">
        Already registered??
        <v-btn class="info" :disabled="!valid" @click="login" style="margin-bottom: 10px">Login</v-btn>
      </p>
    </form>
  </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>
<style>

.appbackground {
  background: url('../assets/images/New.jpg');
  background-size: cover;
  height: 100%;
  width: 100%;



}

</style>


<script>
import router from '../router';
import {APIService} from '../http/APIService';
const apiService = new APIService();

export default {
  name: 'SignUp',
  components : {},
  data() {
    return {
      credentials: {},
      valid: true,
      showMsg: '',
      loading: false,
      isUpdate: false,
      user:{}
    }
  },
  methods: {
    saveUser() {
      apiService.addNewUser(this.user).then(response => {
        if (response.status === 201) {
          this.customer = response.data;
          this.showMsg = "";
          this.$notify({
            title: 'SignUp Successful!!',
            text: 'Please login to proceed'
          });
          router.push('/auth');
        }else{
          this.showMsg = "error";
        }
      }).catch(error => {
        if (error.response.status === 401) {
          router.push("/auth");
        }else if (error.response.status === 400) {
          this.showMsg = "error";
        }
      });
  },
    login() {
      router.push('/auth');
    }
  }
}
</script>
