<template>
  <div id="app">
    <header>
      <h1>Chord transposer</h1>
      <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link> |
        <router-link to="/instructions">Instructions</router-link>
      </div>
    </header>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}


h1 {
  font-size: 20px
}
body {
  background-color: aliceblue;
  /* background-image: url('/assets/images/guitarBackground.jpeg') blue; */
}
</style>
