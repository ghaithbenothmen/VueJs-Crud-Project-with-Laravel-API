
<script >

import { RouterLink, RouterView } from 'vue-router'
import axios from "axios";
const URL="http://localhost:3000/users";
export default {
  name: "App",
  data() {
    return {
      users: [],
      user: {},
      email: '',
      name: ''
    };
  },
  methods: {
    async getUsers() {
      try {
        const users = await axios.get(
          "http://localhost:3000/users"
        );

        this.users = users.data;
      } catch (e) {
        console.log(e);
      }
    },

    async storeUser() {
      try {
        const user = await axios.post(
          "http://localhost:3000/users", { name: this.name, email: this.email }
        );

        console.log(user)
      } catch (e) {
        console.log(e);
      }
    },

    async updateUser() {
      try {
        const user = await axios.put(
          "http://localhost:3000/users/" + this.user.id,
          {
            name: this.user.name,
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
      this.user.name = user.name;
      this.user.email = user.email;
      this.user.id = user.id;
    },

    async deleteUser(id) {
      let x = window.confirm("You want to delete the user?");

      if (x) {
        const user = await axios.delete(
          "http://localhost:3000/users/" + id
        );

        console.log(user);
        alert("User deleted!");
      }
    },
  },
};



</script>
<!--show users with json-->
  <template>
    <h1>This is First page </h1>
<br>
<div>
  <RouterLink type="button"  to="/showuser" class=" btn btn-info">Show User</RouterLink>
  </div>
  <div>
  <RouterLink to="/adduser" class=" btn btn-dark">Add User</RouterLink>
</div>
<RouterView />
</template>



