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

function cp(char) {
  if (codePoint < 0x10000) {
    s = String.fromCharCode(codePoint);
  } else {
    var offset = codePoint - 0x10000;
    s = String.fromCharCode(0xd800 + (offset >> 10), 0xdc00 + (offset & 0x3ff));
  }
}

function codePoints(text) {
  const points = [];
  // `for .. of` is needed because JS strings are utf-16.
  // Other iteration methods like for(i;;) will iterate over bytes
  // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/codePointAt#looping_with_codepointat
  for (let codePoint of text) {
    points.push(codePoint);
  }
  return points;
}

function charToHex(char) {
  return padToFour(char.codePointAt(0).toString(16).toUpperCase());
  // const hex = "▄".codePointAt(0).toString(16);
  // const result = "\\u" + "0000".substring(0, 4 - hex.length) + hex;
  // return result;
}

function padToFour(textNumber) {
  if (textNumber.length <= 3) {
    textNumber = ("000" + textNumber).slice(-4);
  }
  return textNumber;
}

function copyTextToClipboard(text) {
  // https://stackoverflow.com/questions/400212/how-do-i-copy-to-the-clipboard-in-javascript
  var textArea = document.createElement("textarea");
  //
  // *** This styling is an extra step which is likely not required. ***
  //
  // Why is it here? To ensure:
  // 1. the element is able to have focus and selection.
  // 2. if the element was to flash render it has minimal visual impact.
  // 3. less flakyness with selection and copying which **might** occur if
  //    the textarea element is not visible.
  //
  // The likelihood is the element won't even render, not even a
  // flash, so some of these are just precautions. However in
  // Internet Explorer the element is visible whilst the popup
  // box asking the user for permission for the web page to
  // copy to the clipboard.
  //

  // Place in the top-left corner of screen regardless of scroll position.
  textArea.style.position = "fixed";
  textArea.style.top = 0;
  textArea.style.left = 0;

  // Ensure it has a small width and height. Setting to 1px / 1em
  // doesn't work as this gives a negative w/h on some browsers.
  textArea.style.width = "2em";
  textArea.style.height = "2em";

  // We don't need padding, reducing the size if it does flash render.
  textArea.style.padding = 0;

  // Clean up any borders.
  textArea.style.border = "none";
  textArea.style.outline = "none";
  textArea.style.boxShadow = "none";

  // Avoid flash of the white box if rendered for any reason.
  textArea.style.background = "transparent";

  textArea.value = text;

  document.body.appendChild(textArea);
  textArea.focus();
  textArea.select();

  try {
    var successful = document.execCommand("copy");
    var msg = successful ? "successful" : "unsuccessful";
    console.log("Copying text command was " + msg);
  } catch (err) {
    console.log("Oops, unable to copy");
  }

  document.body.removeChild(textArea);
}
</script>

<template>
  <textarea
    v-model="message"
    class="input-area"
    placeholder="add multiple lines"
    rows="4"
    cols="50"
  ></textarea>

  <table>
    <tr>
      <th>Text</th>
      <th>Codepoint</th>
      <th>More info</th>
      <th>Copy</th>
    </tr>
    <tr class="char" v-for="char in codePoints(message)">
      <td>{{ char }}</td>
      <td>{{ charToHex(char) }}</td>
      <!-- {{ char.codePointAt(0).toString(16) }} <br /> -->
      <!-- charCodeAt: -->
      <!-- {{ char.charCodeAt(0).toString(16) }} <br /> -->
      <td><a :href="'https://unicodeplus.com/U+' + charToHex(char)">info</a></td>
      <td><button @click="copyTextToClipboard(char)">Copy</button></td>
    </tr>
  </table>

  <pre>
    {{ message }}
  </pre>
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
  /* display: inline-block; */
  border: 1px solid #000;
  padding: 2px;
}

.input-area {
  margin: auto;
}
</style>
