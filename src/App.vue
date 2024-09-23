<template>
  <div id="app">
    <nav>
      <div>
        <i class="fa-solid fa-headset"></i> Games opinion
      </div>
      <div>
        <i class="fa-solid fa-house"></i>
        <router-link to="/">Home</router-link>
      </div>
      
    </nav>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

nav {
  display: grid;
  grid-template-columns: max-content max-content;
  justify-content: space-between;
  background-color: #2c2f33;
  padding: 10px;
  color: #fff;
}

nav a {
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  margin-left: 4px;
}

nav a.router-link-exact-active {
  text-decoration: underline;
}
</style>
