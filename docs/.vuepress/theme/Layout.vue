<template>
  <div class="wrapper">

    <Navbar :logo="$site.themeConfig.logo" :sticky="$route.path === '/'" />
    <main>
      <template v-if="$route.path === '/'">
        <Home />
      </template>

      <template v-else>
        <News />
      </template>
    </main>

    <Footer />

  </div>
</template>

<style lang="scss">
@import url('./fonts.scss');

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Open Sans', sans-serif;
    font-size: 16px;
    background: black;
    color: white;
}

header {
    background: black;
}

a {
    color: white;
    text-decoration: none;
}
</style>
