<template>
  <div id="app" class="w-full h-full">
    <div id="nav">
      <!-- <router-link to="/">Home</router-link> | -->
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
@import url("./assets/tailwind.css");
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css");

:root {
  --rblack: hsl(0, 0%, 10%);
  --rorange: hsl(18, 89%, 58%);
  --rgrey88: hsl(0, 0%, 88%);
  --regrey63: hsl(0, 0%, 63%);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
