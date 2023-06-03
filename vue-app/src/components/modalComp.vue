<script>
export default {
  name: 'ModalComp',
  props: {
    message: {
      type: String,
      default: () => '',
    },
    isOpen: {
      type: Boolean,
      default: () => false,
    },
  },
  methods: {
    onNo() {
      this.$emit('handleNo');
    },
    onYes() {
      this.$emit('handleYes');
    },
  },
};
</script>

<template>
  <div id="modal" class="modal" :class="{ 'is-active': isOpen }">
    <div class="modalComp-background"></div>
    <div class="modalComp-card">
      <header class="modalComp-card-head">
        <p class="modalComp-card-title">Confirm</p>
      </header>
      <section class="modalComp-card-body">{{ message }}</section>
      <footer class="modalComp-card-foot">
        <button class="button modal-no" @click="onNo">No</button>
        <button class="button is-primary modal-yes" @click="onYes">Yes</button>
      </footer>
    </div>
  </div>
</template>
