<template>
  <div class="drag-drop-area"></div>
</template>

<script lang="ts" setup>
import {DragDropManager} from '@dnd-kit/dom';
import {Sortable} from '@dnd-kit/dom/sortable';

const props = defineProps<{ images: string[] }>();

onMounted(() => {
  const manager = new DragDropManager();
  const wrapper = document.querySelector('.drag-drop-area');

  if (!wrapper) {
    return;
  }

  props.images.forEach((image, index) => {
    const element = document.createElement('img');
    element.src = image;
    new Sortable({
      id: `image-${index}`,
      index,
      element,
      transition: {
        duration: 250, // Animation duration in ms
        easing: 'cubic-bezier(0.25, 1, 0.5, 1)', // Animation easing
        idle: false, // Whether to animate when no drag is in progress
      }
    }, manager);

    wrapper.appendChild(element);
  });
})
</script>

<style>
.drag-drop-area {
  display: flex;
  gap: 8px;
  padding: 8px;
  border: 1px solid #ccc;
}
.drag-drop-area img {
  width: 200px;
  height: 200px;
}
</style>
