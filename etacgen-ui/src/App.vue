<template>
  <div id="app">
    <!-- <header>HEADER</header>
    <nav>NAV</nav> -->
    <router-view/>
    <!-- <footer>FOOTER</footer> -->
  </div>
</template>

<script>

export default {
  name: 'App'
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2, h3, h4 {
  padding: 0; margin: 0;
}

.layout.horizontal,
.layout.vertical {
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
}
.layout.horizontal {
  -ms-flex-direction: row;
  -webkit-flex-direction: row;
  flex-direction: row;
}
.layout.vertical {
  -ms-flex-direction: column;
  -webkit-flex-direction: column;
  flex-direction: column;
}
.layout.center,
.layout.center-center {
  -ms-flex-align: center;
  -webkit-align-items: center;
  align-items: center;
}
.layout.center-justified,
.layout.center-center {
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
}

.flex-auto {
  -ms-flex: 1 1 auto;
  -webkit-flex: 1 1 auto;
  flex: 1 1 auto;
}

</style>
