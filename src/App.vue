<script setup lang="ts">
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { invoke } from '@tauri-apps/api/core';
import { ref } from 'vue';

const greetMsg = ref('');
const name = ref('');

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
  greetMsg.value = await invoke('greet', { name: name.value });
}
</script>

<template>
  <main class="flex flex-col items-center gap-2">
    <h1 class="text-xl">Welcome to Tauri + Vue</h1>

    <div class="flex flex-row">
      <a href="https://vitejs.dev" target="_blank">
        <img src="/vite.svg" class="logo vite" alt="Vite logo" />
      </a>
      <a href="https://tauri.app" target="_blank">
        <img src="/tauri.svg" class="logo tauri" alt="Tauri logo" />
      </a>
      <a href="https://vuejs.org/" target="_blank">
        <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
      </a>
    </div>

    <p>Click on the Tauri, Vite, and Vue logos to learn more.</p>

    <form class="flex flex-row gap-2 mt-2" @submit.prevent="greet">
      <Input id="greet-input" v-model="name" placeholder="Enter a name..." />
      <Button type="submit">Greet</Button>
    </form>
    <p>{{ greetMsg }}</p>
  </main>
</template>
