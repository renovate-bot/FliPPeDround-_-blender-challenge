<script setup lang="ts">
const props = defineProps<{ name: string }>()
</script>

<template>
  <back />
  <gltfBox :src="`/modules/${props.name}`" />
</template>
