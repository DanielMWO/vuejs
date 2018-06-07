<template>
   <div>
       <label>Zaloguj się e-mailem</label>
       <input @keyup="checkform()" type="email" v-model="email">
       <button 
              :disabled="thereAreErrors"
              @click="enter()">{{buttonLabelToDisplay}}</button>
        <p v-if="errors.length">
            <b>Popraw następujący bład:</b>
             <ul>
               <li v-for="error in errors" :key="error.id">{{ error }}</li>
            </ul>
        </p>      
   </div>
</template>

<script>
export default {
  props: ["buttonLabel"],

  data() {
    return {
      email: "",
      errors: []
    };
  },
  methods: {
    enter() {
      this.$emit("login", this.email);
    },
    checkform() {
      this.errors = [];
      if (!this.email) {
        this.errors.push("Wymagany adres email.");
      } else if (!this.validEmail(this.email)) {
        this.errors.push("Wymagany poprawny format email.");
      }
      if (!this.errors.length) return true;
      //e.preventDefault();
    },
    validEmail: function(email) {
      var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    }
  },
  computed: {
    buttonLabelToDisplay() {
      return this.buttonLabel || "Zaloguj się";
    },
    thereAreErrors() {
      if (this.errors.length) {
        return true;
      }
    }
  }
};
</script>