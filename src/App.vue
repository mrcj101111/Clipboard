<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>

  export default {
    name: 'App'
  }

</script>

<style lang="scss">

  @import './scss/main.scss';

  body {
    background: var(--default-bg);
  }

</style>
