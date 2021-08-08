<template>
  <div>
    <header>
      <router-link to="/">
        <h1><span>Movie</span>Search</h1>
      </router-link>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;600;700&display=swap");
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Poppins", sans-serif;

    &::selection {
      background: transparentize(#42b883, 0.5);
    }
  }
  body {
    background-color: #fff;
  }

  a {
    text-decoration: none;
  }

  header {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 16px;
    background-color: #fff;
    background: linear-gradient(70deg, blue, pink);
  }
  h1 {
    color: #00b489;
    span {
      color: yellowgreen;
    }
  }
</style>
