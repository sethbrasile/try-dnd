<script lang="ts" setup>
const images = [
  '17',
  '29',
  '16',
  '12',
];
</script>

<template>
  <div>
    <NuxtRouteAnnouncer />
    <DragDropArea :images="images" />
  </div>
</template>
