<template>
  <div class="max-w-lg bg-gray-200 mx-auto space-y-10 p-10">
    <h1 class="text-3xl font-bold">@headlessui/vue 1.6.6</h1>
    <p>
      With 1.6.6 enter
      <b>transitions are broken</b>
      and there are issues with focus management when combined with menu.
    </p>
    <div class="flex justify-between space-x-5">
      <div class="space-y-3 flex-1">
        <button type="button" class="secondary" @click="DialogRef.openModal">
          Open Dialog
        </button>
        <button type="button" class="secondary" @click="FormRef.openModal">
          Open Form
        </button>
      </div>
      <Menu />
    </div>
    <p>
      Open a Dialog by @click on a button correctly focuses 1st focusable
      element within the modal.
    </p>
    <p>
      But this doesn't work when buttons are MenuItems in a dropdown. Even when
      trying to focus() elements manually. Hit "Tab" several times until you get
      focus within the Dialog. Now Focus is trapped.
    </p>
    <label class="space-x-2 flex items-center">
      <input
        type="checkbox"
        v-model="fixFocus"
        class="focus:ring-blue-500 h-5 w-5 text-blue-600 border-gray-300 rounded"
      />
      <span class="text-normal select-none">Try manual focus fix</span>
    </label>
    <a
      href="#"
      class="p-2 block focus:outline-none focus:ring focus:ring-red-500 rounded"
    >
      I get Focus
    </a>
    <a
      href="#"
      class="p-2 block focus:outline-none focus:ring focus:ring-red-500 rounded"
    >
      Me too... but next is Modal
    </a>
  </div>

  <Dialog ref="DialogRef">
    I am a DialogModal opened from a
    <b>button</b>
  </Dialog>

  <Dialog ref="FormRef" :focusOn="InputRef">
    <input type="text" ref="InputRef" class="text-normal p-2.5" />
  </Dialog>
</template>

<script setup>
import { ref } from 'vue'
import { fixFocus } from './shared/fixState'
import Menu from './components/Menu.vue'
import Dialog from './components/Dialog.vue'

const DialogRef = ref()
const FormRef = ref()
const InputRef = ref()
</script>
