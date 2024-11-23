<template>
  <div>
    <OpenButton @open="showModal = true" />
    <Modal
      v-if="showModal"
      title="Выберите папку"
      :visible="showModal"
      @close="closeModal"
      @confirm="confirmSelection"
    >
      <FolderTree :folders="mockFolders" @select="handleSelection" />
    </Modal>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import OpenButton from './components/OpenButton.vue'
import Modal from './components/TheModal.vue'
import FolderTree from './components/FolderTree.vue'
import { mockFolders } from './mockFolders'

export default defineComponent({
  components: { OpenButton, Modal, FolderTree },
  setup() {
    const showModal = ref(false)
    const selectedFolder = ref<number | null>(null)

    const closeModal = () => (showModal.value = false)

    const confirmSelection = () => {
      console.log('Выбранная папка:', selectedFolder.value)
      closeModal()
    }

    const handleSelection = (folderId: number) => {
      selectedFolder.value = folderId
    }

    return { showModal, closeModal, confirmSelection, handleSelection, mockFolders }
  },
})
</script>

<style>
body {
  font-family: Arial, sans-serif;
}
</style>
