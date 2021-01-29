<template>
  <div id="app">
    <Header />
    <Container />
  </div>
</template>

<script>
import Header from './components/Header'
import Container from './components/Container'

export default {
  name: 'App',
  components: {
    Header,
    Container,
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  outline: 0;
  border: none;
  list-style-type: none;
  font-family: "Trebuchet MS";
}
html, body{
  width: 100%;
  height: 100%;
  background-color: #123;
}
button{
  cursor: pointer;
}
#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 1140px;
  height: 100%;
  margin: auto;
  /* background-color: #323425; */
}
</style>
