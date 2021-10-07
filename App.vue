<template>
<div id="nav">
  <router-link :to="{name:'Home'}" >Home</router-link>
  <router-link :to="{name:'About'}"  >About</router-link>
</div>
 <transition
    name="custom-classes-transition"
    enter-active-class="animated bounceInUp"
    leave-active-class="animated fadeOut"
  >
  <router-view></router-view>
</transition>
</template>

<script>
export default {
  name: "App"
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: cursive, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  box-sizing: border-box;
}
.container {
  width: 85%;
  margin: auto;
}

#nav{
  display: block;
  margin: 6px auto;
}

#nav a {
  text-decoration: none;
  font-size: 20px;
  margin: 5px;
  transition: all 0.5s;
}

#nav a:hover {
  color: blue;
}

.router-link-active {
  color: rgb(17, 235, 10);
  border-bottom: 3px solid green;
}
</style>
