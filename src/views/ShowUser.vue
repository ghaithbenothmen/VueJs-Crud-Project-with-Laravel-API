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

  created(){
    this.getUsers();
  },
  methods: {
    async getUsers() {
      try {
        const users = await axios.get(
          "http://127.0.0.1:8000/api/profils"
        );

        this.users = users.data;
      } catch (e) {
        console.log(e);
      }
    },

    async storeUser() {
      try {
        const user = await axios.post(
          "http://127.0.0.1:8000/api/profils", { name: this.name, email: this.email }
        );

        console.log(user)
      } catch (e) {
        console.log(e);
      }
    },

    async updateUser() {
      try {
        const user = await axios.put(
          "http://127.0.0.1:8000/api/profils/" + this.user.id,
          {
            nom: this.user.nom,
            email: this.user.email,
          }
        );

        console.log(user.data);
        alert("User updated!");
      } catch (e) {
        console.log(e);
      }
    },

    async editUser(user) {
      this.user.nom = user.nom;
      this.user.email = user.email;
      this.user.id = user.id;
    },

    async deleteUser(id) {
      let x = window.confirm("You want to delete the user?");

      if (x) {
        const user = await axios.delete(
          "http://127.0.0.1:8000/api/profils/" + id
        );
        this.getUsers();
        console.log(user);
        alert("User deleted!");
        window.location.href('/showuser');
      }
    },
  },
};



</script>

<template>
     <div>
      <br>
    <button @click="getUsers" class="btn btn-primary mb-2">Get users</button> <br />
    
    <table  class="table-bordered">
      
      <tr>
        <th scope="col">Nom</th>
        <th scope="col">Email</th>
        <th scope="col" colspan="2">Action</th>
      </tr>
      <tbody class="table-hover">
      <tr class="users" v-for="user in users" :key="user.id">
       
        <td>{{ user.nom }}</td>
        <td>{{ user.email }}</td>
        <td><router-link :to="{name: 'edituser', params: { id: user.id }}" class="btn btn-success">Edit</router-link></td>
        
        <td><button type="button" @click="deleteUser(user.id)" class="btn btn-danger">Delete</button></td>

      </tr>
    </tbody>
  </table>
</div>



  </template>