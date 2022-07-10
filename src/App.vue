<template>
  <div class="max-w-lg bg-gray-200 mx-auto space-y-10 p-10">
    <h1 class="text-3xl font-bold">@headlessui/vue 1.6.4</h1>
    <p>
      With 1.6.4 enter and leave transitions work fine, but there are issues
      with focus management.
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
      But this doesn't work when buttons are MenuItems in a dropdown. Workaround
      is to call focus "manually" in the dialog component.
    </p>
    <label class="space-x-2 flex items-center">
      <input
        type="checkbox"
        v-model="fixFocus"
        class="focus:ring-blue-500 h-5 w-5 text-blue-600 border-gray-300 rounded"
      />
      <span class="text-normal select-none">Apply manual focus fix</span>
    </label>
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
