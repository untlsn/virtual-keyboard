<script setup lang="ts">
  const props = defineProps<{
    text?: string,
    longClick?: boolean
  }>();

  const emit = defineEmits<{
    (emit: 'keydown', key?: string): void
  }>();

  const interval = ref(null as any);

  const ev = () => emit('keydown', props.text);

  const mousedown = () => {
    if (props.longClick) {
      interval.value = setInterval(ev, 100);
    }
  };

  const mouseup = () => {
    if (props.longClick) {
      clearInterval(interval.value);
    }
  };
</script>

<template>
  <div 
    class="h-12 w-8 bg-gray-300 text-2xl flex items-center justify-center rounded-lg cursor-pointer select-none hover:bg-gray-400"
    @click="ev"
    @mousedown="mousedown"
    @touchstart="mousedown"
    @mouseup="mouseup"
    @touchend="mouseup"
  >
    <slot>{{ text }}</slot>
  </div>
</template>