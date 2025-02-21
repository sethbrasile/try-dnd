<script lang="ts" setup>
const images = [
  'https://picsum.photos/id/17/200',
  'https://picsum.photos/id/29/200',
  'https://picsum.photos/id/16/200',
  'https://picsum.photos/id/12/200',
];
</script>

<template>
  <div>
    <NuxtRouteAnnouncer />
    <DragDropArea :images="images" />
  </div>
</template>
