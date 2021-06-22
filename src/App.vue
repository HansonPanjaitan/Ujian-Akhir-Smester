<template>
  <div id="app">
    <div id="nav">
      <div class="h-24 text-gray-100  flex flex-row pb-2"> 
        <div class="flex flex-row text-gray-200 text-xl font-extrabold pl-6 pt-4" style="">
          <router-link to="/">Home</router-link> 
        </div>
        <div class="flex flex-row text-gray-200 text-3xl font-black tracking-wide" style="padding-left: 420px; padding-top: 28px">
          <router-link to="/covid">Aplikasi Data Covid</router-link> 
        </div>
      </div>
    </div>
  <router-view/>
  </div>
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
  background-color: #42b400;
}

#nav a.router-link-exact-active {
  color: springgreen;
}
</style>
