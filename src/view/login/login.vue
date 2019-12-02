<style lang="less">
  @import './login.less';
</style>

<template>
  <div class="login">
    <div class="login-con">
      <div class="loginLogo"></div>
      <Card icon="log-in" title="欢迎登录" :bordered="false">
        <div class="form-con">
          <login-form :loading="loading"  @on-success-valid="handleSubmit"></login-form>
        </div>
      </Card>
    </div>
  </div>
</template>

<script>
import LoginForm from '_c/login-form'
import { mapActions } from 'vuex'
import md5 from 'md5'
export default {
  data () {
    return {
      loading: false
    }
  },
  components: {
    LoginForm
  },
  methods: {
    ...mapActions([
      'handleLogin'
    ]),//,'getUserInfo'
    handleSubmit ({ username, password }) {
      this.loading = true;
      password = md5(password);
      this.handleLogin({ username, password }).then(res => {
        if (res.data.result =='ok'){
          console.log(this.$config)
          this.$router.push({
            path: '/'//this.$config.homeName
          })
        }else{
          this.$Notice.error({
            title: res.data.message
          })
          this.loading = false;
        }
      })
    }
  }
}
</script>

<style>

</style>
