<template>
  <div style="width: 400px; height: 200px; line-height: 45px; border: 1px solid #a0a0a06b; margin-left: 40%; padding-top: 40px;">
    <div>
      <span>用户名：</span>
      <input type="text" v-model="loginForm.username" placeholder="请输入用户名">
    </div>
    <div>
      <span>密 码：</span>
      <input type="password" v-model="loginForm.password" placeholder="请输入密码">
    </div>
    <div>
      <button v-on:click="login">登 录</button>
    </div>
  </div>
</template>

<script>
    export default {
        name: "Login",
        data(){
            return {
                loginForm: {
                    username: '',
                    password: '',
                },
                responseResult: []
            }
        },
        methods: {
          login () {
            this.$axios
              .post('/login', {
                  username: this.loginForm.username,
                  password: this.loginForm.password
              }).
              then(successResonse => {
                  if(successResonse.data.code == 200) {
                    this.$router.replace({path:'/index'})
                  }
              })
              .catch(failResponse => {
                  console.log(failResponse);
              })
          }
        }
    }
</script>

<style scoped>

</style>
