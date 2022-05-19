<template>
  <div id="app">
    <QuoteContainer/>
  </div>
</template>

<script>
import QuoteContainer from "./components/QuoteContainer"

export default {
  name: 'App',
  components: {
    QuoteContainer
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
html,body{
  width: 100%;
  height: fit-content;
}
body{
  background: linear-gradient(135deg,#666669, #4d5153 , #252424);
}
#app {
  width: 100%;
  height: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
