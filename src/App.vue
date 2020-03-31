<template>
  <div class="flexible-content">
    <!--Navbar-->
    <mdb-navbar class="flexible-navbar" color="stylish" position="top" dark href="#" transparent scrolling>
        <mdb-navbar-brand href="#" target="_blank"><strong>Demo Project</strong></mdb-navbar-brand>
        <mdb-navbar-toggler  style="max-width: 1140px">
        <mdb-navbar-nav left>
          <router-link to="/home">
            <mdb-nav-item waves-fixed active class="active" icon="home"></mdb-nav-item>
          </router-link>
        
        </mdb-navbar-nav>
        <mdb-navbar-nav right>
          <div v-if="!currentUser" class="navbar-nav ml-auto">
            <router-link to="/register" @click.native="activeItem = 1">
              <mdb-nav-item
              :action="true"
              :class="activeItem === 1 && 'active'"
              ><mdb-icon icon="user"/><strong>Sign Up</strong></mdb-nav-item>
            </router-link>
            <router-link to="/login" @click.native="activeItem = 2">
              <mdb-nav-item
              :action="true"
              :class="activeItem === 2 && 'active'"
              ><mdb-icon icon="sign-in-alt"/><strong>Login</strong></mdb-nav-item>
            </router-link>
          </div>

          <div v-if="currentUser" class="navbar-nav ml-auto">
            <router-link to="/profile" @click.native="activeItem = 1">
              <mdb-nav-item
              :action="true"
              :class="activeItem === 1 && 'active'"
              ><mdb-icon icon="user"/><strong>{{ currentUser.username }}</strong></mdb-nav-item>
            </router-link>
            <mdb-nav-item href @click.prevent="logOut">
                <mdb-icon icon="sign-out-alt"/>Log Out
            </mdb-nav-item>
          </div>

          <mdb-nav-item> | </mdb-nav-item>
          <mdb-nav-item href="https://www.linkedin.com/in/hanifah-perdilla-onissa-42a014165/" waves-fixed
            ><mdb-icon fab class="text-black" icon="linkedin"
          /></mdb-nav-item>
          <mdb-nav-item href="https://www.instagram.com/azkaahanifah/" waves-fixed
            ><mdb-icon fab icon="instagram"
          /></mdb-nav-item>
          <mdb-nav-item
            href="https://github.com/xalamander13"
            waves-fixed
            class="border border-light rounded mr-1"
            target="_blank"
            ><mdb-icon fab icon="github" class="mr-2" />My GitHub
          </mdb-nav-item>
        </mdb-navbar-nav>
      </mdb-navbar-toggler>
    </mdb-navbar>
    <!--/.Navbar-->
    <router-view />
  </div>
</template>

<script>
  import {
    mdbNavbar,
    mdbNavbarBrand,
    mdbNavbarToggler,
    mdbNavbarNav,
    mdbNavItem
  } from "mdbvue";

  export default {
    name: 'App',
    component: {
      mdbNavbar,
      mdbNavbarBrand,
      mdbNavbarToggler,
      mdbNavbarNav,
      mdbNavItem
    },
    data() {
      return {
        activeItem: 1
      };
    },
    beforeMount() {
      this.activeItem = this.$route.matched[0].props.default.page
    },
    computed: {
      currentUser() {
      return this.$store.state.auth.user;
    }},
    methods: {
      logOut() {
        this.$store.dispatch('auth/logout');
        this.$router.push('/login');
      }
    }
  }
</script>

<style lang="scss">
$image-path: '~@/../mdb/mdbvue/img';
@import '~@/../mdb/mdbvue/scss/mdb-free.scss';

@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap');
</style>

<style scoped>
main {
  background-color: ghostwhite;
}

.flexible-content {
  transition: padding-left 0.3s;
  padding-right: 0px;
}

.flexible-navbar {
  transition: padding-left 0.5s;
  padding-left: 270px;
}
</style>