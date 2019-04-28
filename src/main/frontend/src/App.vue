<template>
  <div id="app">
    <h1>
      <img src="./assets/logo.svg" alt="Enroller" class="logo">
      System do zapisÃ³w na zajÄ™cia
    </h1>
    <div v-if="authenticatedUsername">
      <h2>Witaj {{ authenticatedUsername }}!
        <a @click="logout()" class="float-right  button-outline button">Wyloguj</a>
      </h2>
      <meetings-page :username="authenticatedUsername"></meetings-page>
    </div>
    <div v-else>
      <button @click="registering =false">Zaloguj sie</button>
      <button @click="registering =true">Zarejestruj sie</button>
      <login-form @login="login($event)"
      v-if="!registering"></login-form>
      <login-form @login="register($event)"
      button-label="Zarejestruj sie"
      v-else></login-form>
    </div>
  </div>
</template>

<script>
    import "milligram";
    import LoginForm from "./LoginForm";
    import MeetingsPage from "./meetings/MeetingsPage";

    export default {
        components: {LoginForm, MeetingsPage},
        data() {
            return {
                authenticatedUsername: "",
                registering: false
            };
        },
        methods: {
            login(user) {
                this.authenticatedUsername = user.login;
            },
            logout() {
                this.authenticatedUsername = '';
            },
            register(user) {
            	 this.$http.post('participants', user)
            	     .then(response => {
            	         // uda³o siê
            	     })
            	     .catch(response => {
            	         // nie uda³o sie     
            	     });
            	}
        }
    };
</script>

<style>
  #app {
    max-width: 1000px;
    margin: 0 auto;
  }

  .logo {
    vertical-align: middle;
  }
</style>

