<template>
  <div id="nav">
    <router-link to="/">
      <img class="logo" src="./assets/marvel-logo.png" alt="Marvel logo">
    </router-link> 
    <router-link to="/about">About</router-link>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 10px 45px 5px 28px;
  background: #333;
  margin-bottom: 35px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#nav a {
  font-weight: bold;
  color: #FFF;
  
}

#nav a.router-link-exact-active {
  color: #df635f;
}
.logo{
  height: 50px;
}
</style>
