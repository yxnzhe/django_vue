<template>
  <div id="wrapper">
    <nav class="navbar is-light">
      <div class="navbar-brand"></div>
      <router-link to="/" class="navbar-item"><strong>MiDAgS™</strong></router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
  @import '../node_modules/bulma';
</style>