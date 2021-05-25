<template>
  <TransitionRoot as="template" :show="open">
    <Dialog
      as="div"
      static
      class="fixed inset-0 z-10 overflow-y-auto"
      :open="open"
      @close="$emit('close-modal')"
    >
      <div
        class="flex items-end justify-center min-h-screen px-4 pt-4 pb-20 text-center sm:block sm:p-0"
      >
        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="ease-in duration-200"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <DialogOverlay class="fixed inset-0 transition-opacity bg-gray-500 bg-opacity-75" />
        </TransitionChild>

        <!-- This element is to trick the browser into centering the modal contents. -->
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          enter-to="opacity-100 translate-y-0 sm:scale-100"
          leave="ease-in duration-200"
          leave-from="opacity-100 translate-y-0 sm:scale-100"
          leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
        >
          <div
            class="inline-block px-4 pt-5 pb-4 overflow-hidden text-left align-bottom transition-all transform bg-white rounded-lg shadow-xl sm:my-8 sm:align-middle sm:max-w-lg sm:w-full sm:p-6"
          >
            <header class="flex justify-center mb-4">
              <slot name="icon"></slot>
            </header>
            <main class="flex justify-center text-center">
              <slot></slot>
            </main>
            <footer class="mt-5 sm:mt-6 sm:grid sm:grid-cols-2 sm:gap-3 sm:grid-flow-row-dense md:">
              <slot name="buttons"></slot>
            </footer>
          </div>
        </TransitionChild>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script lang="ts">
import {
  Dialog,
  DialogOverlay,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue';

export default {
  components: {
    Dialog,
    DialogOverlay,
    TransitionChild,
    TransitionRoot,
  },
  props: {
    open: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['close-modal'],
};
</script>
