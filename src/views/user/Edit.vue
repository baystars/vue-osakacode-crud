<template>
  <div class="edit">
    <h1>ユーザ編集</h1>
    <div><input v-model="user.name" placeholder="ユーザ名" /></div>
    <div><input v-model="user.password" placeholder="パスワード" /></div>
    <div><input v-model="user.email" placeholder="メールアドレス" /></div>
    <button @click="editUser($route.params.userId)">更新</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Edit",
  data() {
    return {
      user: {
        name: "",
        password: "",
        email: "",
      },
    };
  },
  created() {
    console.log("aaaa");
    const vm = this;
    axios
      .get("http://localhost:8000/users/" + this.$route.params.userId)
      .then((response) => {
        vm.user = response.data;
      });
  },
  methods: {
    editUser(userId) {
      const vm = this;
      const params = {
        id: userId,
        name: this.user.name,
        password: this.user.password,
        email: this.user.email,
      };
      axios
        .patch("http://localhost:8000/users/update", params)
        .then((response) => {
          vm.$router.push("/");
        });
    },
  },
};
</script>
