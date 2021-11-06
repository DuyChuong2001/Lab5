Skip to content
Search or jump to…
Pull requests
Issues
Marketplace
Explore
 
@DuyChuong2001 
quockhangtran2001
/
lab5-ct449
Public
1
00
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
lab5-ct449/frontend/src/App.vue
@quockhangtran2001
quockhangtran2001 lab5 final
…
Latest commit 1a84dbb 1 minute ago
 History
 1 contributor
63 lines (58 sloc)  1.62 KB
   
<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <a href="/" class="navbar-brand">Ứng dụng Quản lý danh bạ</a>

      <div v-if="currentUser" class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link to="/contactbook" class="nav-link">
            Danh bạ <i class="fas fa-address-book"></i>
          </router-link>
        </li>
      </div>

      <div v-if="!currentUser" class="navbar-nav ml-auto">
        <li class="nav-item">
          <router-link to="/register" class="nav-link"> Đăng ký </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/login" class="nav-link"> Đăng nhập </router-link>
        </li>
      </div>

      <div v-if="currentUser" class="navbar-nav ml-auto">
        <li class="nav-item">
          <router-link to="/profile" class="nav-link">
            {{ currentUser.username }}
          </router-link>
        </li>
        <li class="nav-item">
          <a class="nav-link" @click.prevent="logout"> Đăng xuất </a>
        </li>
      </div>
    </nav>
    <div class="container mt-3">
      <router-view />
    </div>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from "vuex";
export default {
  name: "App",
  computed: {
    ...mapGetters({
      currentUser: "loggedInUser",
    }),
  },
  methods: {
    ...mapMutations([
      "initAuthState", // map this.initAuthState() to this.$store.commit("initAuthState")
    ]),
    logout() {
      this.$store.commit("logout");
      this.$router.push("login");
    },
  },
  mounted() {
    this.initAuthState();
  },
};
</script>
