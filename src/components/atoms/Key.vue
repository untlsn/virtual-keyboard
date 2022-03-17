<script setup lang="ts">
  defineProps<{
    text?: string,
  }>();

  const emit = defineEmits<{
    (emit: 'keydown', key?: string): void
  }>();
</script>

<template>
  <div 
    class="h-12 w-8 bg-gray-300 text-2xl flex items-center justify-center rounded-lg cursor-pointer select-none hover:bg-gray-400"
    @click="emit('keydown', text)"
  >
    <slot>{{ text }}</slot>
  </div>
</template>