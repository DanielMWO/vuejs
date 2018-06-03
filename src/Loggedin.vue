<template>
    <div>  

    <h2>Wtaj  {{email.toLowerCase()}} </h2>
    <p><button @click="logout()">Wyloguj</button></p>
    

    </div>
</template>

<script>



export default {
    props:  ["email"],

    methods: {
     logout() {
      this.$emit('logout')
    }

}

}
</script>

