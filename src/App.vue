<template>
  <div class="wrapper">
    <LoginComponent v-if="!log" @clicked="onLogin" class="login" content="Ink Inc." logoimg="{{getImgUrl(logo)}}"/>
    <InkApp logoimg="{{getImgUrl(logo)}}" v-if="log"/>
  </div>
</template>

<script>
import LoginComponent from './components/major/LoginComponent.vue'
import InkApp from './components/major/InkApp.vue'

export default {
  name: 'App',
  data(){
    return {
      log: true    
    }
  },
  components: {
    LoginComponent,
    InkApp
  },
  methods: {
    getImgUrl(logo) {
      return require("./assets/ident/" + logo);
    },
    onLogin(loginData) {
      this.log = loginData;
    }
  }
}
</script>

<style lang="scss">

@import './assets/ident/ident.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $grey-text;
}
.wrapper {
  height: 97vh;
  background-color: $secondary-color;
  background-image: url(./assets/ident/ink_background.png);
  display: flex;
  align-items: center;
  justify-content: flex-end;
  background-size: cover;
  .login {
    margin: auto 0;
    width: 20%;
    float: right;
  }
}
</style>
