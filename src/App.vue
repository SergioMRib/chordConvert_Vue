<template>
  <div id="app">
    <header>
      <h1>Chord transposer</h1>

      <font-awesome-icon class="menu-bars" icon="bars" v-on:click="hideNav"/>
      <div id="nav" class="hidden" v-on:click="hideNav">
        <p><router-link to="/">Home</router-link></p>
        <p><router-link to="/about">About</router-link></p>
        <p><router-link to="/instructions">Instructions</router-link></p>
      </div>
    </header>
    <router-view/>
  </div>
</template>

<script>
export default {
  methods: {
    hideNav: function () {
      console.log("The hamburger works")
      document.getElementById("nav").classList.toggle("hidden")
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(177, 234, 248);
  margin-top: 0px;
  font-size: 20px;
}

header {
  display: grid;
  grid-template-columns: 1fr 8fr 1fr;
  justify-items: stretch;
  align-items: stretch;
}

h1 {
  margin-top: 0px;
  margin-left: 1em;
  font-size: 1em;
  text-align: left;
  display: inline;
}

#nav {
  position: fixed;
  right: 0;
  top: 40px;
  width: 40%;
  margin: 3px;
  padding: 10px 5px 10px 5px;
  background-color: #698c7b;
  border-radius: 5px;
}
.hidden {
  visibility: hidden;
}
.svg-inline--fa {
    font-size: 1.5em;
}
.menu-bars {
  grid-column-end: -1;
}

a {
  line-height: 3em;
  color: white;
  text-decoration: none;
}

body {
  margin: 5px 0px 0px 0px;
  background-color: rgb(57, 73, 96);
  /* background-image: url('/assets/images/guitarBackground.jpeg') blue; */
}


</style>
