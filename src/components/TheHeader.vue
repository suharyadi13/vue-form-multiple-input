<template>
  <nav class="navbar is-black">
    <div class="navbar-menu">
      <div class="navbar-start">
        <router-link to="/" class="navbar-item">
          Home
        </router-link>
        <router-link to="/form-multiple" class="navbar-item">
          Form Multiple
        </router-link>
      </div>
    </div>
  </nav>  
</template>

<script>
export default {
  name: "TheHeader",
};
</script>
