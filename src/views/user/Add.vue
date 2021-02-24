<template>
  <div class="add">
    <h1>ユーザ作成</h1>
    <div><input v-model="user.name" placeholder="ユーザ名" /></div>
    <div><input v-model="user.password" placeholder="パスワード" /></div>
    <div><input v-model="user.email" placeholder="メールアドレス" /></div>
    <button @click="addUser">新規作成</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Add",
  data() {
    return {
      user: {
        name: "",
        password: "",
        email: "",
      },
    };
  },
  methods: {
    addUser() {
      const vm = this;
      const params = {
        name: this.user.name,
        password: this.user.password,
        email: this.user.email,
      };
      axios.post("http://localhost:8000/users/add", params).then((response) => {
        vm.$router.push("/");
      });
    },
  },
};
</script>
