<template>
  <div class="w-full px-2 sm:px-0">
    <TabGroup>
      <TabList class="flex space-x-2 rounded-xl bg-blue-400 p-2">
        <Tab as="template" v-slot="{ selected }">
          <button
            :class="[
              'w-full rounded-lg py-2.5 text-xl font-medium leading-5 text-blue-700',
              'ring-white ring-opacity-60 ring-offset-2 ring-offset-blue-400 focus:outline-none focus:ring-2',
              selected
                ? 'bg-white shadow'
                : 'text-blue-100 hover:bg-white/[0.12] hover:text-white',
            ]"
          >
            Preview
          </button>
        </Tab>
        <Tab as="template" v-slot="{ selected }">
          <button
            :class="[
              'w-full rounded-lg py-2.5 text-xl font-medium leading-5 text-blue-700',
              'ring-white ring-opacity-60 ring-offset-2 ring-offset-blue-400 focus:outline-none focus:ring-2',
              selected
                ? 'bg-white shadow'
                : 'text-blue-100 hover:bg-white/[0.12] hover:text-white',
            ]"
          >
            Get The Code
          </button>
        </Tab>
      </TabList>
      <TabPanels class="mt-2">
        <TabPanel
          :class="[
            'rounded-xl bg-white p-3',
            'ring-white ring-opacity-60 ring-offset-2 ring-offset-blue-400 focus:outline-none focus:ring-2',
          ]"
        >
          <div class="overflow-hidden rounded-lg bg-white shadow">
            <div class="px-4 py-5 sm:p-6">
              <div class="border-l-4 border-yellow-400 bg-yellow-50 p-4 mb-4">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <ExclamationTriangleIcon
                      class="h-5 w-5 text-yellow-400"
                      aria-hidden="true"
                    />
                  </div>
                  <div class="ml-3">
                    <p class="text-sm text-yellow-700">
                      This preview <strong>intentionally</strong> disables the
                      Keyboard Events mapping.<br />
                      (You can't use your keyboard to interact with the
                      preview.)
                    </p>
                  </div>
                </div>
              </div>
              <div
                ref="preview"
                id="preview"
                class="w-full"
                v-html="code"
              ></div>
            </div>
            <div
              class="bg-gray-50 px-4 py-4 sm:px-6 sm:flex sm:flex-row-reverse"
            >
              <button
                type="button"
                @click="open"
                class="inline-flex items-center rounded-md border border-transparent bg-blue-500 px-3 py-2 text-sm font-medium leading-4 text-white shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
              >
                Edit
              </button>
            </div>
          </div>
        </TabPanel>
        <TabPanel
          :class="[
            'rounded-xl bg-white p-3',
            'ring-white ring-opacity-60 ring-offset-2 ring-offset-blue-400 focus:outline-none focus:ring-2',
          ]"
        >
          <div class="overflow-hidden rounded-lg bg-white shadow">
            <div class="px-4 py-5 sm:p-6 prose prose-2xl max-w-full">
              <div class="border-b border-gray-200 bg-white px-4 py-5 sm:px-6">
                <h2 class="mt-0 text-xl font-medium leading-6 text-gray-900">
                  <strong>1:</strong> Add the Wordle For Good script to the
                  <span class="text-blue-700">&lt;head&gt;</span> of your page
                </h2>
                <pre><code class="language-html">&lt;script defer src="{{ script }}"&gt;&lt;/script&gt;</code></pre>
              </div>
              <div class="bg-white px-4 py-5 sm:px-6">
                <h2 class="mt-0 text-xl font-medium leading-6 text-gray-900">
                  <strong>2:</strong> Add the Wordle For Good code where you
                  want the game to load
                </h2>
                <pre><code class="language-javascript">{{ codeField }}</code></pre>
              </div>
            </div>
            <div
              class="bg-gray-50 px-4 py-4 sm:px-6 sm:flex sm:flex-row-reverse gap-4"
            >
              <button
                type="button"
                @click="copyCode"
                class="inline-flex items-center rounded-md border border-transparent bg-blue-500 px-3 py-2 text-sm font-medium leading-4 text-white shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
              >
                Copy Code
              </button>
              <button
                type="button"
                @click="copyScript"
                class="inline-flex items-center rounded-md border border-transparent bg-blue-500 px-3 py-2 text-sm font-medium leading-4 text-white shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
              >
                Copy Script
              </button>
            </div>
          </div>
        </TabPanel>
      </TabPanels>
    </TabGroup>
  </div>
</template>

<script setup lang="ts">
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from "@headlessui/vue";
import { ExclamationTriangleIcon } from "@heroicons/vue/20/solid";
import { ref } from "vue";

const script = ref(
  "https://apps.4sitestudios.com/wordle-for-good/wordle-for-good.js"
);

const preview = ref();
const code = ref();
const codeField = ref();

const emit = defineEmits(["open", "alert"]);

function open() {
  emit("open");
}
function loadPreview(customElement: string) {
  code.value = `<wordle-for-good ${customElement} keyboard-events=false></wordle-for-good>`;
  codeField.value = `<wordle-for-good ${customElement}></wordle-for-good>`;
}

function copyScript() {
  navigator.clipboard.writeText(
    `<script defer src="${script.value}"></${"script"}>`
  );
  emit("alert", "Script copied to clipboard");
}
function copyCode() {
  navigator.clipboard.writeText(codeField.value);
  emit("alert", "Code copied to clipboard");
}
defineExpose({ loadPreview });
</script>
