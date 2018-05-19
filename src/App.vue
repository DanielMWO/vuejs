<template>
  <div id="app">
    <h1>Witaj w systemie zapisów na zajęcia</h1>
    
    <div v-if= "logedin == false" >
      <p>zaloguj się e-mailem: <input type="email" v-model="email">
      <button @click="loginByEmail()">Zaloguj</button></p>
    </div>
    <div v-if="logedin == true" >
      <h1>Wtaj</h1>
      <p>Twój email to :{{email.toLowerCase()}}
      <button @click="logoutByEmail()">Wyloguj</button></p>
    </div>
    
    
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      email: "jakis@email.pl",
      logedin: false,
    };
  },
  methods: {
    loginByEmail() {
      this.logedin = true;
    },
    logoutByEmail() {
      this.logedin = false;
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
