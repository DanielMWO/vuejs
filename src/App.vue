<template>
  <div id="app">
    <h1>Witaj w systemie zapisów na zajęcia</h1>
    
    <div v-if = "!authenticatedEmail">
      <login-form @login = "loginByEmail($event)" 
                  :button-label ="'Wchodzę'" ></login-form>

                  <login-form @login = "loginByEmail($event)" 
                  :button-label ="'Loguję'" ></login-form>
                  
                  <login-form @login = "loginByEmail($event)" 
                  :button-label ="'OK'" ></login-form>
                  
                  <login-form @login = "loginByEmail($event)" 
                  :button-label ="'itp'" ></login-form>
    </div>

    <div v-else>
      <h2>Wtaj  {{authenticatedEmail.toLowerCase()}} </h2>
     <!-- <p><button @click="logoutByEmail()">Wyloguj</button></p> -->
     <p><a href="" @click="logoutByEmail()">Wyloguj</a></p>
    </div>
    
    
  </div>
</template>

<script>
import "milligram";
import LoginForm from "./LoginForm";

export default {
  components: {LoginForm},
  name: "app",
  data() {
    return {
      authenticatedEmail: '',
      
    };
  },
  methods: {
    loginByEmail(email) {
      this.authenticatedEmail = email;
    },
    logoutByEmail() {
      this.authenticatedEmail = '';
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
