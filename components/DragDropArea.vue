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

  props.images.forEach((imageId, index) => {
    const element = document.createElement('img');
    element.src = `https://picsum.photos/id/${imageId}/200`;
    element.id = imageId;
    new Sortable({
      id: imageId,
      index,
      element,
      transition: {
        duration: 250, // Animation duration in ms
        easing: 'cubic-bezier(0.25, 1, 0.5, 1)', // Animation easing
        idle: false, // Whether to animate when no drag is in progress
      }
    }, manager);

    wrapper?.appendChild(element);

    manager.monitor.addEventListener('dragend', (event) => {
      const { source, target, canceled } = event.operation;
      if (!canceled && target) {
        // would update data here but source and target ID are the same?
        // bug? doing something wrong? this lib isn't 1.0 yet
        console.log(source?.id, target.id);
      }
    });
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
