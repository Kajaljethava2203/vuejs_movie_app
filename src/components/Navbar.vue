<template>
 <nav>
<div class="menu-item"><a href="Popular_movie">Popular Movie</a></div>
<div class="menu-item"><a href="Trending_movie">Trending Movie</a></div>
</nav>
</template>

<script>
export default {
}
</script>

<style>
nav {
  display: flex;
  align-items: center;
  justify-content: center;
}

nav .menu-item {
  color: #FFF;
  padding: 10px 20px;
  position: relative;
  text-align: center;
  font-size: 20px;
  border-bottom: 3px solid transparent;
  display: flex;
  transition: 0.4s;
}

nav .menu-item.active,
nav .menu-item:hover {
  background-color: #444;
  border-bottom-color: #FF5858;
}

nav .menu-item a {
  color: inherit;
  text-decoration: none;
}
</style>