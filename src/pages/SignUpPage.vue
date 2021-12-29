<template>
   <form>
      <h1>Sign Up</h1>
      <label for="username">Username</label>
      <input id="username" v-model="username" />

      <label for="e-mail">E-mail</label>
      <input id="e-mail" v-model="email" />

      <label for="password">Password</label>
      <input id="password" type="password" v-model="password" />

      <label for="password-repeat">Password Repeat</label>
      <input id="password-repeat" type="password" v-model="passwordRepeat" />

      <button :disabled="isDisabled" @click.prevent="submit">Sign Up</button>
   </form>
</template>

<script>
// import axios from "axios";

export default {
   name: "SignUpPage",
   data() {
      return {
         username: "",
         email: "",
         password: "",
         passwordRepeat: "",
      };
   },
   methods: {
      //It's possible to prevent submit event by adding @click.prevent
      submit() {
         const requestBody = {
            username: this.username,
            email: this.email,
            password: this.password,
         }
         // axios.post("/api/1.0/users", {
         //    username: this.username,
         //    email: this.email,
         //    password: this.password,
         // });
         fetch("/api/1.0/users", {
            method: "POST",
            body: JSON.stringify(requestBody),
            headers:{
               "Content-type": "application/json"
            }
         })
      },
   },
   computed: {
      isDisabled() {
         return this.password && this.passwordRepeat
            ? this.password != this.passwordRepeat
            : true;
      },
   },
};
</script>