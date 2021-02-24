<template>
  <div class="home">
    <h1>ユーザ一覧</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }} {{ user.email }}
        <router-link tag="button" :to="'/user/edit/' + user.id"
          >編集</router-link
        >
        <button @click="deleteUser(user.id)">削除</button>
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
  data() {
    return {
      users: [],
    };
  },
  created() {
    this.reloadUsers();
  },
  methods: {
    deleteUser(userId) {
      let vm = this;
      this.$axios
        .delete("http://localhost:8000/users/" + userId)
        .then((response) => {
          vm.reloadUsers();
        });
    },
    reloadUsers() {
      let vm = this;
      this.$axios.get("http://localhost:8000/users").then((response) => {
        vm.users = response.data;
      });
    },
  },
};
</script>
