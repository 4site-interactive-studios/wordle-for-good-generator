<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = false">
      <div class="fixed inset-0" />

      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16">
            <TransitionChild as="template" enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full" enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700" leave-from="translate-x-0"
              leave-to="translate-x-full">
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <div class="flex h-full flex-col divide-y divide-gray-200 bg-white shadow-xl">
                  <div class="h-0 flex-1 overflow-y-auto">
                    <div class="bg-indigo-700 py-6 px-4 sm:px-6">
                      <div class="flex items-center justify-between">
                        <DialogTitle class="text-lg font-medium text-white">Edit Wordle</DialogTitle>
                        <div class="ml-3 flex h-7 items-center">
                          <button type="button"
                            class="rounded-md bg-indigo-700 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white"
                            @click="open = false">
                            <span class="sr-only">Close panel</span>
                            <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                          </button>
                        </div>
                      </div>
                      <div class="mt-1">
                        <p class="text-sm text-indigo-300">
                          Get started by filling in the information below to
                          create your wordle game.
                        </p>
                      </div>
                    </div>
                    <div class="flex flex-1 flex-col justify-between">
                      <div class="divide-y divide-gray-200 px-4 sm:px-6">
                        <div class="space-y-6 pt-6 pb-5">
                          <div>
                            <label for="game-title" class="block text-sm font-medium text-gray-900">Game Title</label>
                            <div class="mt-1">
                              <input v-model="title" type="text" name="game-title" id="game-title"
                                class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="share-title" class="block text-sm font-medium text-gray-900">Share Title</label>
                            <div class="mt-1">
                              <input v-model="shareTitle" type="text" name="share-title" id="share-title"
                                class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="target-word" class="block text-sm font-medium text-gray-900">Target Word</label>
                            <div class="mt-1">
                              <input v-model="targetWord" type="text" name="target-word" id="target-word" maxlength="5"
                                class="uppercase block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="success-selector" class="block text-sm font-medium text-gray-900">Success
                              Selector</label>
                            <div class="mt-1">
                              <input v-model="successSelector" type="text" name="success-selector" id="success-selector"
                                class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                            <p class="mt-2 text-sm text-gray-500" id="email-description">
                              Query selector for the element that has the
                              content to show when the game is won.
                            </p>
                          </div>
                          <div>
                            <label for="failure-selector" class="block text-sm font-medium text-gray-900">Failure
                              Selector</label>
                            <div class="mt-1">
                              <input v-model="failureSelector" type="text" name="failure-selector" id="failure-selector"
                                class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                            <p class="mt-2 text-sm text-gray-500" id="email-description">
                              Query selector for the element that has the
                              content to show when the game is lost.
                            </p>
                          </div>
                          <div>
                            <label for="bg-color" class="block text-sm font-medium text-gray-900">Game Background
                              Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="bgColor" format="hex" shape="circle" useTypes="hex" />
                              </div>
                              <input v-model="bgColor" type="text" name="bg-color" id="bg-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="text-color" class="block text-sm font-medium text-gray-900">Text Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="textColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="textColor" type="text" name="text-color" id="text-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="tile-border-color" class="block text-sm font-medium text-gray-900">Tile Border
                              Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="tileBorderColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="tileBorderColor" type="text" name="tile-border-color"
                                id="tile-border-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="tile-bg-color" class="block text-sm font-medium text-gray-900">Tile Background
                              Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="tileBgColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="tileBgColor" type="text" name="tile-bg-color" id="tile-bg-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="tile-text-color" class="block text-sm font-medium text-gray-900">Tile Text
                              Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="tileTextColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="tileTextColor" type="text" name="tile-text-color" id="tile-text-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="key-bg-color" class="block text-sm font-medium text-gray-900">Key Background
                              Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="keyBgColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="keyBgColor" type="text" name="key-bg-color" id="key-bg-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="key-text-color" class="block text-sm font-medium text-gray-900">Key Text
                              Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="keyTextColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="keyTextColor" type="text" name="key-text-color" id="key-text-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="keyboard-text-size" class="block text-sm font-medium text-gray-900">Keyboard
                              Font Size</label>
                            <div class="mt-1">
                              <input v-model="keyTextSize" type="text" name="keyboard-text-size" id="keyboard-text-size"
                                class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="tile-bg-wrong-color" class="block text-sm font-medium text-gray-900">Wrong
                              Letter Background Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="tileBgWrongColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="tileBgWrongColor" type="text" name="tile-bg-wrong-color"
                                id="tile-bg-wrong-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="tile-bg-correct-color" class="block text-sm font-medium text-gray-900">Right
                              Letter Background Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="tileBgCorrectColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="tileBgCorrectColor" type="text" name="tile-bg-correct-color"
                                id="tile-bg-correct-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="tile-bg-wrong-color" class="block text-sm font-medium text-gray-900">Right
                              Letter Wrong Location Background Color</label>
                            <div class="relative mt-1">
                              <div class="absolute inset-y-0 left-2 flex items-center">
                                <ColorPicker v-model:pureColor="tileBgWrongLocationColor" format="hex" shape="circle"
                                  useTypes="pure" />
                              </div>
                              <input v-model="tileBgWrongLocationColor" type="text" name="tile-bg-wrong-location-color"
                                id="tile-bg-wrong-location-color"
                                class="pl-9 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                          <div>
                            <label for="game-height" class="block text-sm font-medium text-gray-900">Game Board
                              Height</label>
                            <div class="mt-1">
                              <input v-model="gameHeight" type="text" name="game-height" id="game-height"
                                class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" />
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="flex flex-shrink-0 justify-end px-4 py-4">
                    <button type="button"
                      class="rounded-md border border-gray-300 bg-white py-2 px-4 text-sm font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                      @click="open = false">
                      Cancel
                    </button>
                    <button @click="save" type="submit"
                      class="ml-4 inline-flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                      Save
                    </button>
                  </div>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup lang="ts">
import { ref, onMounted, onUpdated, onBeforeUpdate, watch } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";
// import the component

const open = ref(true);
const title = ref("Wordle For Good");
const shareTitle = ref(null);
const targetWord = ref("HEART");
const successSelector = ref();
const failureSelector = ref();

const bgColor = ref("#fafafa");
const textColor = ref("#333333");
const tileBorderColor = ref("#888888");
const tileBgColor = ref("#ffffff");
const tileBgWrongColor = ref("#39393c");
const tileBgWrongLocationColor = ref("#b59f3b");
const tileBgCorrectColor = ref("#538d4e");
const tileTextColor = ref("#333333");
const keyBgColor = ref("#818283");
const keyTextColor = ref("#ffffff");
const keyTextSize = ref("1.3rem");
const gameHeight = ref("700px");

const openModal = () => {
  open.value = true;
};

const getWord = () => {
  return targetWord.value
    .split("")
    .map((letter) => {
      return letter.toLowerCase().charCodeAt(0);
    })
    .join("-");
};

const getCode = () => {
  let code = `
  word="${getWord()}"
  bg-color="${bgColor.value}"
  text-color="${textColor.value}"
  tile-border-color="${tileBorderColor.value}"
  tile-bg-color="${tileBgColor.value}"
  tile-bg-wrong-color="${tileBgWrongColor.value}"
  tile-bg-wrong-location-color="${tileBgWrongLocationColor.value}"
  tile-bg-correct-color="${tileBgCorrectColor.value}"
  tile-text-color="${tileTextColor.value}"
  key-bg-color="${keyBgColor.value}"
  key-text-color="${keyTextColor.value}"
  key-text-size="${keyTextSize.value}"
  height="${gameHeight.value}"`;
  if (title.value) {
    code += `\n  title="${title.value}"`;
  }
  if (shareTitle.value) {
    code += `\n  share-title="${shareTitle.value}"`;
  }
  if (successSelector.value) {
    code += `\n  success-selector="${successSelector.value}"`;
  }
  if (failureSelector.value) {
    code += `\n  failure-selector="${failureSelector.value}"`;
  }

  return code;
};

const save = () => {
  saveToLocalStorage();
  emit("save", getCode());
  open.value = false;
};

const saveToLocalStorage = () => {
  const data = {
    title: title.value,
    shareTitle: shareTitle.value,
    word: targetWord.value,
    successSelector: successSelector.value,
    failureSelector: failureSelector.value,
    bgColor: bgColor.value,
    textColor: textColor.value,
    tileBorderColor: tileBorderColor.value,
    tileBgColor: tileBgColor.value,
    tileBgWrongColor: tileBgWrongColor.value,
    tileBgWrongLocationColor: tileBgWrongLocationColor.value,
    tileBgCorrectColor: tileBgCorrectColor.value,
    tileTextColor: tileTextColor.value,
    keyBgColor: keyBgColor.value,
    keyTextColor: keyTextColor.value,
    keyTextSize: keyTextSize.value,
    gameHeight: gameHeight.value,
  };
  localStorage.setItem("wordle-for-good", JSON.stringify(data));
};

const loadFromLocalStorage = () => {
  const data = localStorage.getItem("wordle-for-good");
  if (data) {
    const parsed = JSON.parse(data);
    title.value = parsed.title;
    shareTitle.value = parsed.shareTitle;
    targetWord.value = parsed.word;
    successSelector.value = parsed.successSelector;
    failureSelector.value = parsed.failureSelector;
    bgColor.value = parsed.bgColor;
    textColor.value = parsed.textColor;
    tileBorderColor.value = parsed.tileBorderColor;
    tileBgColor.value = parsed.tileBgColor;
    tileBgWrongColor.value = parsed.tileBgWrongColor;
    tileBgWrongLocationColor.value = parsed.tileBgWrongLocationColor;
    tileBgCorrectColor.value = parsed.tileBgCorrectColor;
    tileTextColor.value = parsed.tileTextColor;
    keyBgColor.value = parsed.keyBgColor;
    keyTextColor.value = parsed.keyTextColor;
    keyTextSize.value = parsed.keyTextSize;
    gameHeight.value = parsed.gameHeight;
  }
};

defineExpose({ openModal, getCode });
const emit = defineEmits(["save"]);
onMounted(() => {
  loadFromLocalStorage();
  emit("save", getCode());
});
onBeforeUpdate(() => {
  saveToLocalStorage();
  emit("save", getCode());
});
watch(
  () => [
    title.value,
    shareTitle.value,
    targetWord.value,
    successSelector.value,
    failureSelector.value,
    bgColor.value,
    textColor.value,
    tileBorderColor.value,
    tileBgColor.value,
    tileBgWrongColor.value,
    tileBgWrongLocationColor.value,
    tileBgCorrectColor.value,
    tileTextColor.value,
    keyBgColor.value,
    keyTextColor.value,
    keyTextSize.value,
    gameHeight.value,
  ],
  () => {
    saveToLocalStorage();
    emit("save", getCode());
  }
);
</script>
