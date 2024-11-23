<template>
  <div v-if="visible" class="modal-overlay" @click.self="close">
    <div class="modal">
      <h3>{{ title }}</h3>
      <slot></slot>
      <div class="modal-buttons">
        <button @click="close">Закрыть</button>
        <button @click="confirm">Ок</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    title: {
      type: String,
      required: true,
    },
    visible: {
      type: Boolean,
      required: true,
    },
  },
  emits: ['close', 'confirm'],
  setup(_, { emit }) {
    const close = () => emit('close');
    const confirm = () => emit('confirm');

    return { close, confirm };
  },
});
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal {
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
  text-align: center;
}
.modal-buttons {
  margin-top: 20px;
}
button {
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
</style>