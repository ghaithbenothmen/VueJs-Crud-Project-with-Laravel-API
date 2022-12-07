<script >

import axios from "axios";
const URL="http://127.0.0.1:8000/api/profils";
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
  props:{
  id:Number
  },

  created(){
    this.getUsers();
  },
  methods: {
    async getUsers() {
      try {
        const users = await axios.get(
          "http://127.0.0.1:8000/api/profils/"+this.$route.params.id
        );

        this.users = users.data;
      } catch (e) {
        console.log(e);
      }
    },

    

    async updateUser() {
      try {
        const user = await axios.put(
          'http://127.0.0.1:8000/api/profils/'+this.$route.params.id,
          {
            nom: this.user.nom,
            email: this.user.email,
          }
        );

        console.log(user);
        alert("User updated!");
        this.$router.push('/showuser');
        console.log(user);
      } catch (e) {
        console.log(e);
      }
    },

    async editUser(user) {
      this.nom = user.nom;
      this.email = user.email;

    },

   
  },
};



</script>

<template>
    <!--update users with json-->
<div class=" form-group"><br>
    <h2>Update user</h2><br>
    <input type="text" v-model="user.nom" class="form-control" placeholder=" Nom et Prenom"/> <br />
    <input type="text" v-model="user.email" class="form-control" placeholder=" Adresse email"/> <br />

    <button @click="updateUser" class="btn btn-primary mb-2">Update</button>
  </div>

  </template>