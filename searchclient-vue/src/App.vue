<template>
  <div id="app" class="w-full h-screen">
    <nav class="bg-gray-900" id="nav">
      <div class="container mx-auto px-6 py-3 flex justify-between items-end">
        <a class="r-text-orange-brand leading-none text-2xl lg:text-4xl" href="#">reason</a>
        <div class="block lg:hidden">
          <button
            class="flex items-center px-3 py-2 border rounded text-gray-500 border-gray-600 hover:text-gray-800 hover:border-teal-500 appearance-none focus:outline-none"
          >
            <svg
              class="fill-current h-3 w-3"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <title>Menu</title>
              <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z" />
            </svg>
          </button>
        </div>
        <div class="text-blue-400 lg:text-xl hidden lg:block">
          <ul class="inline-flex">
            <!-- <router-link to="/">Home</router-link> | -->
            <li>
              <a class="px-4 font-bold" href="/">Home</a>
            </li>
            <li>
              <a class="px-4 hover:text-gray-800" href="#">About</a>
            </li>
            <li>
              <a class="px-4 hover:text-gray-800" href="#">Contact</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

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

.r-text-orange-brand {
  color: var(--rorange);
}

#app {
  // font-family: Avenir, Helvetica, Arial, sans-serif;
  // -webkit-font-smoothing: antialiased;
  // -moz-osx-font-smoothing: grayscale;
  text-align: center;
  // color: #2c3e50;
}

#nav {
  // padding: 30px;

  a {
    // font-weight: bold;
    // color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
