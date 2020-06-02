<template>
  <div class="home">
    
    <div v-if="user" class="text-secondary text-left">
      Welcome back, 
      <span class="font-weight-bold text-info">{{user.displayName}}</span>, <a
      href="#"
      role="button"
      class="text-primary"
      @click="$emit('logout')"
      >logout</a>
    </div>

  </div>

  
</template>

<script>

export default {
  name: "home",
  props: ["user"]
};

</script>
