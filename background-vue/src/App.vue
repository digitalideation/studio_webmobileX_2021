<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/stories">Story</router-link>
  </div>
  <router-view/>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inria+Serif:wght@300&display=swap');
 body {
            margin: 0;
            padding: 0;
            font-family: 'Inria Serif', Georgia, serif;
            font-size: 1.8rem;
            color: rgb(0, 68, 255);
            background-color: rgba(255, 255, 255, 0.6)
        }
#app {
  margin: 0;
            padding: 0;
            font-family: 'Inria Serif', Georgia, serif;
            font-size: 1.8rem;
            color: rgb(0, 68, 255);
            background-color: rgba(255, 255, 255, 0.6)
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
