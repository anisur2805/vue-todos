<script setup>

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="../assets/logo.svg" width="90" height="90" />

    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
    </div>
  </header>
</template>

<style lang="scss" scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 900px;
  margin: auto;
  padding: 20px 0;
  border-bottom: 1px solid #ddd;
}

nav {
    a {
        padding: 10px;
        font-weight: bold;
        color: #2c3e50;
        text-decoration: none;
        &.router-link-exact-active {
            color: #42b983;
        }
    }
}
</style>
