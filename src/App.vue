<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import InputOutput from "./components/InputOutput.vue";
</script>

<template>
  <header>
    <h1>JS Unicode Debugger</h1>
    <p>
      Paste or type your text into this box then inspect the unicode information
      of each character below. You can share the URL with the debug information
      like these examples:
      <a href="?q=🤷¯\_(ツ)_/¯emoji">(1)</a>
      <a href="?q=monospace?𝚖𝚘𝚗𝚘𝚜𝚙𝚊𝚌𝚎!">(2)</a>
      <a href="?q=ൠ❽ᴥ∰⁂᧻◉✪❤෴">(3)</a>
    </p>
  </header>
  <InputOutput />
  <footer>
    <ul>
      <li>
        <img alt="Unicode" src="./assets/Unicode_sample.png" />
        <img alt="Unicode" src="./assets/New_Unicode_logo.svg" />
      </li>
      <li>
        Learn more about Unicode at
        <a href="https://en.wikipedia.org/wiki/Unicode">Wikipedia</a>
      </li>
      <li>
        Created by
        <a href="https://twitter.com/ubershmekel">ubershmekel</a>
      </li>
      <li>
        See
        <a href="https://github.com/ubershmekel/unicode-debugger"
          >source on github</a
        >
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
