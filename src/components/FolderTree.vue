<template>
  <ul class="folder-tree">
    <li v-for="folder in folders" :key="folder.id">
      <div class="folder-item">
        <span @click="toggle(folder)">{{ isOpen(folder) ? '-' : '+' }}</span>
        <span
          :class="{ selected: selectedFolder === folder.id }"
          @click="selectFolder(folder)"
        >
          {{ folder.name }}
        </span>
      </div>
      <FolderTree
        v-if="isOpen(folder)"
        :folders="folder.children"
        @select="updateSelection"
      />
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, ref, PropType } from 'vue';

interface Folder {
  id: number;
  name: string;
  children: Folder[];
}

export default defineComponent({
  name: 'FolderTree',
  props: {
    folders: {
      type: Array as PropType<Folder[]>,
      required: true,
    },
  },
  emits: ['select'],
  setup(props, { emit }) {
    const openFolders = ref<number[]>([]);
    const selectedFolder = ref<number | null>(null);

    const toggle = (folder: Folder) => {
      const index = openFolders.value.indexOf(folder.id);
      if (index > -1) {
        openFolders.value.splice(index, 1);
      } else {
        openFolders.value.push(folder.id);
      }
    };

    const isOpen = (folder: Folder) => openFolders.value.includes(folder.id);

    const selectFolder = (folder: Folder) => {
      selectedFolder.value = folder.id;
      emit('select', folder.id);
    };

    return { toggle, isOpen, selectFolder, selectedFolder };
  },
});
</script>

<style scoped>
.folder-tree {
  list-style: none;
  padding-left: 20px;
}
.folder-item {
  display: flex;
  align-items: center;
  cursor: pointer;
}
.folder-item span {
  margin-right: 8px;
}
.selected {
  font-weight: bold;
  color: blue;
}
</style>