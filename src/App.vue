<template>
<header class="header">
  <router-link to="">
    <h1>AGA<span>Movie</span></h1>
  </router-link>
</header>
<main>
  <router-view/>
</main>
</template>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:'Fira Sans', sans-serif;

  &::selection{
    background: transparent blue;
  }
}
body{
  background: rgba(0, 0, 255, 0.212);
}
a{
  text-decoration: none;
}
h1{
  color: white;
  font-size:28px;
  span{
    color: green;
  }
}
header{
  display: flex;
  box-shadow: 10px 20px 10px rgb(0, 45, 128);
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background: transparent;
  color: rgb(35, 36, 33);
}

</style>
