<script setup>
defineEmits(['close-modal'])
defineProps({
  modalActive: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <Teleport to="body">
    <Transition name="modal-outer">
      <div v-show="modalActive"
           class="absolute w-full h-screen bg-opacity-30 inset-0 bg-black flex items-center justify-center px-8"
           @click.self="$emit('close-modal')"
      >
        <Transition name="modal-inner">
          <div v-if="modalActive" class="max-w-screen-md bg-slate-50 shadow-lg p-4 rounded-xl top-1/2 left-1/2">
            <slot/>
            <div class="flex justify-end items-end">
              <button
                  class="bg-slate-950 text-slate-50 py-2 px-6 rounded-md hover:bg-slate-900"
                  @click="$emit('close-modal')"
              >
                Close
              </button>
            </div>
          </div>
        </Transition>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.modal-outer-enter-active, .modal-outer-leave-active {
  transition: opacity 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-outer-enter-from, .modal-outer-leave-to {
  opacity: 0;
}

.modal-inner-enter-active {
  transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02) 0.15s;
}

.modal-inner-leave-active {
  transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-inner-enter-from {
  opacity: 0;
  transform: scale(0.8);
}

.modal-inner-leave-to {
  transform: scale(0.8);
}
</style>