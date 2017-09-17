<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
  :root {
    --bg-dark-color: #222;
    --text-light-color: #FFF;
  }

  * {
    margin: 0;
    padding: 0;
  }
</style>
