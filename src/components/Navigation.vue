<template>
  <nav class="navbar navbar-expand bg-primary navbar-dark">
    <div class="container-fluid">
      <router-link class="navbar-brand" to="/">RiKiCo</router-link>
        <div class="navbar-nav ml-auto">
          <router-link v-if="user" class="nav-item nav-link" to="/scraps">Scraps</router-link>
          <router-link v-if="!user" class="nav-item nav-link" to="/login">Login</router-link>
          <router-link v-if="!user" class="nav-item nav-link" to="/register">Register</router-link>
          <button class="nav-item nav-link btn btn-link" @click="$emit('logout')">Logout</button>
        </div>
    </div>
  </nav>

</template>

<script>
export default {
  name: "navigation",
  props: ["user"]
}
</script>
