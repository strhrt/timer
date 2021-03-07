<template>
  <div id="app">
    <header class="header">header</header>
    <MainPage />
  </div>
</template>
<script>
export default {
  components: {
    MainPage: () => import('@/views/MainPage')
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: bold;
  color: #202830;
  background-color: #383a3b;

  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100%;
}
.header {
  background-color: orangered;
  height: 60px;
  width: 100%;
}
</style>
