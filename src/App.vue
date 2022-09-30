<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import Page from "./components/Page.vue";
import Form from "./components/Form.vue";
import Alert from "./components/Alert.vue";

import { ref } from "vue";

const form = ref();
const page = ref();
const alert = ref();

function open() {
  form.value.openModal();
}
function loadCode(code: string) {
  page.value.loadPreview(code);
}
function showAlert(message: string) {
  alert.value.showAlert(message);
}
</script>

<template>
  <div class="flex justify-center items-center min-h-screen w-full bg-blue-400">
    <div class="w-full md:w-1/2 bg-white rounded shadow-2xl p-8 m-4 relative">
      <div class="bg-white">
        <div class="mx-auto max-w-7xl py-16 px-4 sm:py-24 sm:px-6 lg:px-8">
          <div class="text-center">
            <img
              src="https://www.4sitestudios.com/wp-content/themes/foursite/images/logos/logo-4siteCloud.svg"
              class="d-block mx-auto"
            />
            <p
              class="mt-1 text-4xl font-bold tracking-tight text-gray-900 sm:text-5xl lg:text-6xl"
            >
              Wordle For Good Generator
            </p>
            <p class="mx-auto mt-5 max-w-xl text-xl text-gray-500">
              Create your own Wordle Game in a few clicks
            </p>
          </div>
        </div>
      </div>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <Alert ref="alert" />
        <!-- Replace with your content -->
        <div class="px-4 py-6 sm:px-0">
          <Page ref="page" @open="open" @alert="showAlert" />
        </div>
        <!-- /End replace -->
      </div>
    </div>
    <Form ref="form" @save="loadCode" />
  </div>
</template>

<style scoped>
@import "https://rsms.me/inter/inter.css";
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
