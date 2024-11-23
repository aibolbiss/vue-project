<template>
  <button @click="openModal">Открыть</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  emits: ['open'],
  setup(_, { emit }) {
    const openModal = () => {
      emit('open');
    };

    return { openModal };
  },
});
</script>

<style scoped>
button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>