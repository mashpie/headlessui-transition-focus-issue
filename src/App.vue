<template>
  <div class="max-w-lg bg-gray-200 mx-auto space-y-10 p-10">
    <h1 class="text-3xl font-bold">@headlessui/vue 1.6.7</h1>
    <p>
      With 1.6.7 enter and leave transitions work fine and all issues with focus
      management are fixed.
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
      And this also works when buttons are MenuItems in a dropdown. No
      workaround needed any more.
    </p>
  </div>

  <Dialog ref="DialogRef">
    I am a DialogModal opened from a
    <b>button</b>
  </Dialog>

  <Dialog ref="FormRef">
    <input type="text" ref="InputRef" class="text-normal p-2.5" />
  </Dialog>
</template>

<script setup>
import { ref } from 'vue'
import Menu from './components/Menu.vue'
import Dialog from './components/Dialog.vue'

const DialogRef = ref()
const FormRef = ref()
</script>
