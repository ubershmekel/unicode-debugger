<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import InputOutput from "./components/InputOutput.vue";
</script>

<template>
  <header>
    <img alt="Unicode" src="./assets/Unicode_sample.png" />
    <img alt="Unicode" src="./assets/New_Unicode_logo.svg" />
  </header>
  <InputOutput />
  <footer>
    <ul>
      <li>
        Learn more about Unicode at a
        <a href="https://en.wikipedia.org/wiki/Unicode">Wikipedia</a>
      </li>
      <li>
        Created by
        <a href="https://twitter.com/ubershmekel">ubershmekel</a>
      </li>
    </ul>
  </footer>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

img {
  height: 30px;
}

footer li {
  list-style-type: none;
}
</style>
