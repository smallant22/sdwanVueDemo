<style lang="less">
  @import './login.less';
</style>

<template>
  <div class="login">
    <div class="login-con">
      <div class="loginLogo"></div>
      <Card icon="log-in" title="欢迎登录" :bordered="false">
        <div class="form-con">
          <login-form :notice="notice" :loading="loading" @on-success-valid="handleSubmit"></login-form>
        </div>
      </Card>
    </div>
  </div>
</template>

<script>
import LoginForm from '_c/login-form'
import { mapActions } from 'vuex'
import md5 from 'md5';
export default {
  data () {
    return {
      notice: '',
      loading: false
    }
  },
  components: {
    LoginForm
  },
  methods: {
    ...mapActions([
      'handleLogin',
      'getUserInfo'
    ]),
    handleSubmit ({ username, password }) {
      this.handleLogin({ username, password }).then(res => {
        debugger
        if (res.data.result =='ok'){
          this.$router.push({
            name: this.$config.homeName
          })
        }else{
          this.notice = res.data.message
          this.loading=false
        }
      })
    }
  }
}
</script>

<style>

</style>
