<template>
  <section v-if="show" class="modal">
    <div
      :class="['backdrop', { 'hide-background': hideBackground }]"
      @click="$emit('onModalBackdropClick')"
    />
    <div
      data-testid="dialog"
      :class="['dialog', { 'hide-background': hideBackground }]"
    >
      <slot name="modal-content" />
    </div>
  </section>
</template>

<script setup>

defineProps({
  show: Boolean,
  hideBackground: Boolean,
})
</script>

<style scoped>
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  overflow-x: hidden;
  overflow-y: auto;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 25;
  height: 100%;
  width: 100%;
}

  .modal .backdrop {
    z-index: 1;
    background-color: rgba(242, 245, 246, 0.9);
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
  }

  .modal .backdrop.hide-background {
    background-color: transparent;
  }

  .modal .dialog {
    z-index: 2;
    background-color: #fff;
    border-radius: 7px;
    box-shadow: 0 2px 4px 0 rgba(35, 35, 35, 0.15);
    position: relative;
    display: flex;
    flex-direction: column;


  }
   .modal .dialog  .hide-background {
      box-shadow: transparent;
    }
  .modal .dialog.hide-background {
    box-shadow: none;
  }

</style>