<template>
  <Menu as="div" class="relative inline-block text-left">
    <div>
      <MenuButton
        class="inline-flex w-full justify-center rounded-md bg-blue-500 px-4 py-2.5 font-medium text-white hover:bg-blue-600 focus:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75"
      >
        Menu Demos
        <ChevronDownIcon
          class="ml-2 -mr-1 h-5 w-5 text-blue-200 hover:text-blue-100"
          aria-hidden="true"
        />
      </MenuButton>
    </div>

    <transition
      enter-active-class="transition duration-100 ease-out"
      enter-from-class="transform scale-95 opacity-0"
      enter-to-class="transform scale-100 opacity-100"
      leave-active-class="transition duration-75 ease-in"
      leave-from-class="transform scale-100 opacity-100"
      leave-to-class="transform scale-95 opacity-0"
    >
      <MenuItems
        class="absolute right-0 mt-2 w-56 origin-top-right divide-y divide-gray-100 rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
      >
        <div class="px-1 py-1">
          <MenuItem v-slot="{ active }">
            <button
              :class="[
                active ? 'bg-blue-500 text-white' : 'text-gray-900',
                'group flex w-full items-center rounded-md px-2 py-2 text-sm'
              ]"
              @click="DialogRef.openModal"
            >
              Open Dialog
            </button>
          </MenuItem>
          <MenuItem v-slot="{ active }">
            <button
              :class="[
                active ? 'bg-blue-500 text-white' : 'text-gray-900',
                'group flex w-full items-center rounded-md px-2 py-2 text-sm'
              ]"
              @click="FormRef.openModal"
            >
              Open Form
            </button>
          </MenuItem>
        </div>
      </MenuItems>
    </transition>
  </Menu>

  <Dialog ref="DialogRef">
    I am a DialogModal opened from a
    <b>menu button</b>
  </Dialog>

  <Dialog ref="FormRef" :focusOn="InputRef">
    <input type="text" ref="InputRef" />
  </Dialog>
</template>

<script setup>
import { ref } from 'vue'
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue'
import { ChevronDownIcon } from '@heroicons/vue/solid'
import Dialog from './Dialog.vue'

const DialogRef = ref()
const FormRef = ref()
const InputRef = ref()
</script>
