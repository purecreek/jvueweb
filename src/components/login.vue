<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-md-4 col-md-push-8">
          <form onsubmit="javascript:return false;" method="post"
                class="fh5co-form animate-box fadeInRight animated-fast" data-animate-effect="fadeInRight"
                autocomplete="off">
            <h2>登陆</h2>
            <div class="form-group">
              <label for="username" class="sr-only">用户名</label>
              <input type="text" v-model="username" class="form-control" id="username" placeholder="用户名"
                     autocomplete="off">
            </div>
            <div class="form-group">
              <label for="password" class="sr-only">密码</label>
              <input type="text" v-model="password" v-on:keyup="changePasswordType" class="form-control" id="password"
                     placeholder="密码"
                     autocomplete="off">
            </div>
            <div class="form-group">
              <label for="remember"><input type="checkbox" v-model="rememberMe" name="remember-me" id="remember"> 记住我</label>
            </div>
            <div class="form-group">
              <p>没有账号? <a href="#">注册</a> | <a href="#">忘记密码?</a></p>
            </div>
            <div class="form-group">
              <button v-on:click="doLogin" class="btn btn-primary">登陆</button>
            </div>
          </form>
          <!-- END Sign In Form -->
        </div>
      </div>
      <div class="row" style="padding-top: 60px; clear: both;">
        <div class="col-md-12 text-center">
          <p>
            <small>© All Rights Reserved. jvue</small>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        username: '',
        password: '',
        rememberMe:''
      }
    },
    methods: {
      changePasswordType: function () {
        /*$("#password").attr("type", "password")*/
      },
      doLogin: function () {

        var login_url = server_host + "/login";
        this.$http.post(login_url, {
          username: this.username,
          password: this.password,
          rememberMe:this.rememberMe,
          permissionId: 1
        }, {credentials: true}).then(
          function (res) {

            if (200 === res.body.state) {
              /*this.$router.push("/main")*/
              this.$store.commit("changeLoginInfo", res.body.data.JSESSIONID);
              this.$store.commit("setuserinfo",res.body.data.userinfo);
            }
            else {

              alert("失败"+this.username+':'+this.password)
            }
          }
          ,

          function (res) {
          }
        )

      }
    }

  }
</script>
<style>

  input:-webkit-autofill {
    -webkit-box-shadow: 0 0 0px 1000px white inset;
    -webkit-text-fill-color: #333;
  }

  body {
    background: #ffffff url(../img/login.png) repeat;
  }

  a {
    color: #33cccc;
    -moz-transition: all 0.3s ease;
    -o-transition: all 0.3s ease;
    -webkit-transition: all 0.3s ease;
    -ms-transition: all 0.3s ease;
    transition: all 0.3s ease;
  }

  a:hover {
    color: #29a3a3;
  }

  .menu {
    padding: 0;
    margin: 30px 0 0 0;
  }

  .menu li {
    list-style: none;
    margin-bottom: 10px;
    display: -moz-inline-stack;
    display: inline-block;
    zoom: 1;
    *display: inline;
  }

  .menu li a {
    padding: 5px;
  }

  .menu li.active a {
    color: #b3b3b3;
  }

  .fh5co-form {
    padding: 30px;
    margin-top: 4em;
    -webkit-box-shadow: -4px 7px 46px 2px rgba(0, 0, 0, 0.1);
    -moz-box-shadow: -4px 7px 46px 2px rgba(0, 0, 0, 0.1);
    -o-box-shadow: -4px 7px 46px 2px rgba(0, 0, 0, 0.1);
    box-shadow: -4px 7px 46px 2px rgba(0, 0, 0, 0.1);
    background: #ffffff;
  }

  @media screen and (max-width: 768px) {
    .fh5co-form {
      padding: 15px;
    }
  }

  .fh5co-form h2 {
    text-transform: uppercase;
    letter-spacing: 2px;
    font-size: 20px;
    margin: 0 0 30px 0;
    color: #000000;
  }

  .fh5co-form .form-group {
    margin-bottom: 30px;
  }

  .fh5co-form .form-group p {
    font-size: 14px;
    color: #9f9f9f;
    font-weight: 300;
  }

  .fh5co-form .form-group p a {
    color: #000000;
  }

  .fh5co-form label {
    font-weight: 300;
    font-size: 14px;
    font-weight: 300;
  }

  .fh5co-form .form-control {
    font-size: 16px;
    font-weight: 300;
    height: 50px;
    padding-left: 0;
    padding-right: 0;
    border: none;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    -webkit-box-shadow: none;
    -moz-box-shadow: none;
    -o-box-shadow: none;
    box-shadow: none;
    -webkit-border-radius: 0px;
    -moz-border-radius: 0px;
    -ms-border-radius: 0px;
    border-radius: 0px;
    -moz-transition: all 0.3s ease;
    -o-transition: all 0.3s ease;
    -webkit-transition: all 0.3s ease;
    -ms-transition: all 0.3s ease;
    transition: all 0.3s ease;
  }

  .fh5co-form .form-control::-webkit-input-placeholder {
    color: rgba(0, 0, 0, 0.3);
    text-transform: uppercase;
  }

  .fh5co-form .form-control::-moz-placeholder {
    color: rgba(0, 0, 0, 0.3);
    text-transform: uppercase;
  }

  .fh5co-form .form-control:-ms-input-placeholder {
    color: rgba(0, 0, 0, 0.3);
    text-transform: uppercase;
  }

  .copyrights {
    text-indent: -9999px;
    height: 0;
    line-height: 0;
    font-size: 0;
    overflow: hidden;
  }

  .fh5co-form .form-control:-moz-placeholder {
    color: rgba(0, 0, 0, 0.3);
    text-transform: uppercase;
  }

  .fh5co-form .form-control:focus, .fh5co-form .form-control:active {
    border-bottom: 1px solid rgba(0, 0, 0, 0.4);
  }

  .btn-primary {
    height: 50px;
    padding-right: 20px;
    padding-left: 20px;
    border: none;
    background: #33cccc;
    color: #ffffff;
    -webkit-box-shadow: -2px 10px 20px -1px rgba(51, 204, 204, 0.4);
    -moz-box-shadow: -2px 10px 20px -1px rgba(51, 204, 204, 0.4);
    -o-box-shadow: -2px 10px 20px -1px rgba(51, 204, 204, 0.4);
    box-shadow: -2px 10px 20px -1px rgba(51, 204, 204, 0.4);
  }

  .btn-primary:hover, .btn-primary:focus, .btn-primary:active {
    color: #ffffff;
    background: #47d1d1 !important;
    outline: none;
  }

  input, textarea {
    color: #000;
  }

  .placeholder {
    color: #aaa;
  }

  .js .animate-box {
    opacity: 0;
  }


</style>


