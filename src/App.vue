<template>
  <div id="app">
    <div class="logo">
        <div class="container"><a href="#"></a></div>
    </div>
    <div class="panel">
        <div class="container">
            <div class="panel-layout">
                <div class="panel-tabs">
                    <a  href="javascript:void(0);" @click="selectTab('login')" class="tabs-link " :class="{select:login}" data-tab="login">账号登录</a>
                    <span class="line"></span>
                    <a  href="javascript:void(0);" @click="selectTab('register')" class="tabs-link" :class="{select:!login}" data-tab="register">账号注册</a>
                </div>
                <div class="panel-account">
                    <form action="javascript:;" method="POST" id="form"  @submit="sumbitForm">
                        <label class="account-label" for="username">
                            <input v-model="loginInfo.userName" class="account-item" autocomplete="off" type="text" name="name" placeholder="账号">
                        </label>
                        <label class="account-label" for="pwd">
                            <input v-model="loginInfo.password" class="account-item" type="password" placeholder="密码" autocomplete="off"
                                name="password">
                        </label>
                        <label v-show="!login" class="account-label password2" for="pwd2" >
                            <input v-model="loginInfo.confirmPwd" class="account-item" type="password" placeholder="重复密码" autocomplete="off"
                                name="password2">
                        </label>
                        <input class="btn" type="submit" :value="loginText">
                    </form>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'




export default {
  name: 'app',
  data(){
    return{
      login:true,
      loginInfo:{
        userName:'',
        password:'',
        confirmPwd:''
      }
    }
  },



  methods:{
    selectTab(tab){
      if(tab =='login'){
        this.login = true;
      }else{
        this.login = false;
      }
    },

    sumbitForm(){
       try {
        if (!this.loginInfo.userName) {
          throw "当前用户名为空，请输入用户名！";
        }
        if (this.login) {
          if (!this.loginInfo.password) {
            throw "当前密码为空，请输入密码!";
          }
        } else {
          if (!this.loginInfo.password || !this.loginInfo.confirmPwd) {
            throw "请输入密码！";
          }
          if (this.loginInfo.confirmPwd !== this.loginInfo.password) {
            throw "两次密码不一致，请重新输入！";
          }
        }
      } catch (e) {
        alert(e);
      }

      if(this.login){
        const param = {
          name:this.loginInfo.userName,
          password:this.loginInfo.password
        }
        axios.post('http://vip.chanke.xyz/mi/login',param).then ((data)=>{console.log(data)},(err)=>{console.log(err)})
      }else{
         const param = {
          name:this.loginInfo.userName,
          password:this.loginInfo.password
        }
        axios.post('http://vip.chanke.xyz/mi/register',param).then ((data)=>{console.log(data)},(err)=>{console.log(err)})
      }
    },

  },

  computed:{
    loginText(){
      return this.login ?'登录':'注册';
    }
  }
 
}
</script>

<style>
     body,
        a {
            margin: 0;
            padding: 0;
        }

        a {
            text-decoration: none;
        }

        .container {
            width: 1130px;
            margin: 0 auto;
        }

        .container::before,
        .container::after,
        .clearfix::before,
        .clearfix::after {
            content: "";
            display: table;
        }

        .container::after,
        .clearfix::after {
            clear: both;
        }

        .logo a {
            display: block;
            background: url(img/mistore_logo.png) no-repeat;
            width: 200px;
            height: 98px;
        }

        .panel {
            background: url(img/loginbg.jpg) no-repeat top center;
            height: 588px;
        }

        .panel-layout {
            width: 410px;
            min-height: 524px;
            background: white;
            margin-top: 32px;
            float: right;
        }


        .panel-tabs {
            padding: 27px 0 24px;
            text-align: center;
            font-size: 24px;
            color: #e0e0e0;
        }

        .panel-tabs .select {
            color: #f56600;
        }

        .panel-tabs .line {
            width: 1px;
            height: 24px;
            margin: 0 35px 0 42px;
            border: 1px solid #e0e0e0;
        }

        .tabs-link {
            padding: 27px 0 24px;
            text-align: center;
            font-size: 24px;
            color: #666;
        }

        .panel-account {
            width: 348px;
            margin: 0 auto;
            margin-top: 10px;
        }

        .account-item {
            width: 306px;
            height: 22px;
            line-height: 22px;
            padding: 13px 16px 13px 14px;
            display: block;
            outline: 0;
            border: 0 none;
            color: #333;
        }

        .account-label {
            margin-bottom: 14px;
            border: 1px solid #e0e0e0;
            outline: 0 none;
            display: -webkit-box;
        }

        .panel-account .btn {
            background-color: #ef5b00;
            width: 100%;
            height: 50px;
            line-height: 50px;
            display: block;
            margin-bottom: 14px;
            text-align: center;
            font-size: 14px;
            color: #fff;
            cursor: pointer;
            border: 0;
            outline: 0;
        }
</style>
