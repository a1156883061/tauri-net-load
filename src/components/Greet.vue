<script setup lang="ts">
import {ref} from "vue";
import {convertFileSrc, invoke} from "@tauri-apps/api/tauri";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg.value = await invoke("greet", {name: name.value});
}

let fileLoadList = ref<string[]>([])

async function add() {
  // change to local file on network driver
  const fileList = [
    // "F:\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (3).jpg",
    // "F:\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (4).jpg",
    // "F:\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (5).jpg",
    // "F:\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (6).jpg",
    // "F:\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (7).jpg",
    // "F:\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (8).jpg",
    "\\\\home.haoyuanlord.net\\media\\OBS\\Screenshot 2023-05-25 19-27-32.png",
    "\\\\home.haoyuanlord.net\\media\\OBS\\Screenshot 2023-05-25 19-27-54.png",
    "\\\\home.haoyuanlord.net\\media\\OBS\\Screenshot 2023-06-05 00-11-09.png",
    "\\\\home.haoyuanlord.net\\media\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (5).jpg",
    "\\\\home.haoyuanlord.net\\media\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (6).jpg",
    "\\\\home.haoyuanlord.net\\media\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (7).jpg",
    "\\\\home.haoyuanlord.net\\media\\漫画\\测试\\pexels-roberto-nickson-2559941 - 副本 (8).jpg",
  ]
  fileLoadList.value = fileList.map(file => convertFileSrc(file))

}

</script>

<template>
  <form class="row" @submit.prevent="greet">
    <input id="greet-input" v-model="name" placeholder="Enter a name..."/>
    <button type="submit">Greet</button>
    <button type="button" @click="add">add</button>
  </form>
  <div>
    <div v-for="(filePath) in fileLoadList">
      <img :src="filePath" width="500">
    </div>
  </div>

  <p>{{ greetMsg }}</p>
</template>
