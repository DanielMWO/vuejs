<template>
    <div>  
        <div>     
         <p>Witaj  {{email.toLowerCase()}}
         <button @click="logout()">Wyloguj</button></p>
         </div>
    </div>
</template>

<script>
export default {
  props: ["email"],

  methods: {
    logout() {
      this.$emit("logout");
    }
  }
};
</script>

