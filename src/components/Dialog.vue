<template>
  <TransitionRoot :show="isOpen" as="template" @after-enter="onEntered">
    <Dialog as="div" @close="closeModal" class="relative z-10">
      <TransitionChild
        as="template"
        enter="duration-300 ease-out"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="duration-200 ease-in"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-black bg-opacity-25" />
      </TransitionChild>

      <div class="fixed inset-0 overflow-y-auto">
        <div
          class="flex min-h-full items-center justify-center p-4 text-center"
        >
          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0 scale-95"
            enter-to="opacity-100 scale-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100 scale-100"
            leave-to="opacity-0 scale-95"
          >
            <DialogPanel
              class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white p-6 text-left align-middle shadow-xl transition-all"
            >
              <DialogTitle
                as="h3"
                class="text-lg font-medium leading-6 text-gray-900"
              >
                Title
              </DialogTitle>
              <div class="mt-2">
                <p class="text-sm text-gray-500">
                  <slot></slot>
                </p>
              </div>

              <div class="mt-6 grid grid-flow-row-dense grid-cols-2 gap-6">
                <button
                  ref="OkButtonRef"
                  type="button"
                  class="primary sm:col-start-2"
                  @click="closeModal"
                >
                  Ok
                </button>
                <button
                  type="button"
                  class="secondary sm:col-start-1"
                  @click="closeModal"
                >
                  Cancel
                </button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from 'vue'
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
  DialogTitle
} from '@headlessui/vue'

import { fixFocus } from '../shared/fixState'

const props = defineProps({
  focusOn: { type: Object },
  fixFocus: { type: Boolean }
})

const isOpen = ref(false)

const closeModal = () => {
  isOpen.value = false
}
const openModal = () => {
  isOpen.value = true
}

const OkButtonRef = ref(null)

const onEntered = () => {
  if (!fixFocus.value) return

  if (props.focusOn) {
    props.focusOn.focus()
  } else {
    OkButtonRef.value.focus()
  }
}

defineExpose({
  closeModal,
  openModal
})
</script>
