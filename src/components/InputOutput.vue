<script setup lang="ts">
import { ref, watch } from "vue";

// defineProps<{ msg: string }>();
const url = new URL(window.location.href);
const firstPageLoadQ = url.searchParams.get("q") || "";
const message = ref(firstPageLoadQ);

watch(() => {
  console.log(message.value);
  const url = new URL(window.location.href);
  url.searchParams.set("q", message.value);
  // window.location.search = url.searchParams;
  // const newUrl = window.location.protocol + "//" + window.location.host + window.location.pathname + '?myNewUrlQuery=1';
  const newUrl = url.toString();
  window.history.pushState({ path: newUrl }, "", newUrl);
});
</script>

<template>
  <textarea
    v-model="message"
    placeholder="add multiple lines"
    rows="4"
    cols="50"
  ></textarea>

  <!-- <button type="button" @click="count++">count is: {{ count }}</button> -->
  <pre>
    {{ message }}
  </pre>

  <ul>
    <li class="char" v-for="char in message">
      {{ char }} <br />
      Codepoint:
      {{ char.codePointAt(0).toString(16) }} <br />
      charCodeAt:
      {{ char.charCodeAt(0).toString(16) }} <br />
    </li>
  </ul>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}

.char {
  display: inline-block;
  border: 1px solid #000;
  padding: 2px;
}
</style>
