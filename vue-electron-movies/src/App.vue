<template>
  <div id="app">
    <div class="container">
      <div class="text-center user-select-none">
        <h2 class="text-center mt-5">{{ new Date().toLocaleString('default', { month: 'long' }) }} {{ new Date().getYear() + 1900 }} Movies 🍿</h2>
        <p>keep up with popular movie trends</p>
      </div>

      <div class="my-4 user-select-none">
        <a href="#" class="mx-3 h4 nounderline"> Trending today</a>
        <a href="#" class="mx-3 h4 nounderline">This week</a>
      </div>
    </div>
  </div>
</template>
<style scoped>
  .nounderline {
    text-decoration: none;
  }
</style>