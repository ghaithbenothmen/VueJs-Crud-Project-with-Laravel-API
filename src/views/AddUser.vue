<script >

import axios from "axios";
const URL="http://localhost:3000/users";
export default {
  name: "adduser",
  data() {
    return {
      users: [],
      user: {},
      email: '',
      nom: ''
    };
  
  },
  methods: {
   

    async storeUser() {
      try {
        const user = await axios.post(
          "http://127.0.0.1:8000/api/profils", { nom: this.nom, email: this.email }
        );
        this.nom="";
        this.email="";
        this.$router.push('/showuser');
        console.log(user);
      } catch (e) {
        console.log(e);
      }
    },

    


    
  },
};



</script>

<template>
   

    <div class=" form-group">
      <br>
    <h2>Add user</h2>
     <br>
    
    <input type="text" v-model="nom" class="form-control" placeholder=" Nom et Prenom"/> <br />
    <input type="text" v-model="email" class="form-control" placeholder=" Adresse mail"/> <br />

    
    <button @click="storeUser" class="btn btn-primary mb-2">Ajouter</button>
  </div>

  </template>