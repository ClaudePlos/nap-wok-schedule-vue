<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/todo">Todo</router-link>
  </div>
  <router-view/>
</template>

<style lang="stylus">

* {
  box-sizing : border-box;
}

#app {
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
}

.home {
  max-width : 600px;
  margin : 0 auto;
}

.todolist {
  max-width : 600px;
  margin : 0 auto;
}

.logo {
  display : block;
  margin : 20px auto;
  height : 75px;
}

</style>
