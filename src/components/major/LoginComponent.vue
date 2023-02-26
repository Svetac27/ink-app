<template>
  <div class="login-wrapper">
    <div class="home-img">
      <img class="logo" :src="getImgUrl(logo)" alt="Ink Logo">
    </div>
    <h3 class="name">{{ident.company_name}}</h3>
    <div class="input-wrapper">
      <div class="username">
        <label for="username">{{msg.username}}</label>
        <input type="text" id="username" name="username" :placeholder="[`${msg.your_username}`]">
      </div>
      <div class="password">
        <label for="password">{{msg.password}}</label>
        <input type="password" id="password" name="password" :placeholder="[`${msg.your_password}`]">
        <button @click="login()" class="btn primary-btn">{{msg.login}}</button>
      </div>
    </div>
  </div>
</template>
<script>
import identification from '../../assets/ident/ident.json';
import msg from '../../assets/data/language_data.json';

export default {
  name: 'HomeComponent',
  props: {
    content: String
  },
  data() {
    return {
      ident: identification,
      msg: msg.en,
      message: msg,
      logo: identification.logo
    }
  },
  methods: {
    getImgUrl(logo) {
      return require("../../assets/ident/" + logo);
    },
    login() {
      this.$emit('clicked', true)
    }
  }
}

</script>
<style lang="scss" scope>
@import '../../assets/css/style.scss';
.login-wrapper {
  background-color: $primary-color;
  padding: 20px;
  .home-img {
    display: flex;
    justify-content: right;
  }
  .name {
    margin: 50px 0;
  }
  .input-wrapper {
    padding: 40% 0;
    .username,
    .password {
      label {
        float: left;
        margin-bottom: 10px;
        color: $grey-text;
        font-size: 14px;
      }
      input {
        padding: 10px;
        width: 90%;
        height: 20px;
        margin-bottom: 10px;
        border-radius: 5px;
        border: none;
      }
      input::placeholder {
        color: $grey-text;
        font-size: 14px;
      }
      .btn {
        margin: 20px 0;
        width: 100%;
        font-weight: 600;
        cursor: pointer;
      }
    }
  }
}

</style>