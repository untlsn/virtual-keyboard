<script setup lang="ts">

const letterKeys = [
  'qwertyuiop'.split(''),
  'asdfghjkl'.split(''),
  'zxcvbnm'.split(''),
];


const text = ref('');
const uppercaseStore = reactive({
  one: false,
  two: false,
});

watch(
  () => text.value,
  () => {
    if (uppercaseStore.one && !uppercaseStore.two) uppercaseStore.one = false;
  },
);

const uppercase = computed(() => uppercaseStore.one);

const setUppercase = () => {  
  if (uppercaseStore.one) {
    if (uppercaseStore.two) {
      uppercaseStore.one = false;
      uppercaseStore.two = false;
    } else {
      uppercaseStore.two = true;
    }
  } else {
    uppercaseStore.one = true;
  }
};

</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen">
    <textarea :value="text" rows="5" />
    <div class="flex flex-col items-center gap-1 relative" :class="{ uppercase }">
      <div v-for="(keysLine, index) in letterKeys" :key="index" class="flex gap-1">
        <Key
          v-for="key in keysLine"
          :key="key"
          :text="key"
          @keydown="key => text += uppercase ? key?.toUpperCase() : key"
        />
      </div>
      <Key class="absolute left-0 bottom-0 w-12" @keydown="setUppercase">
        Shf
      </Key>
      <Key class="absolute right-0 bottom-0 w-12" long-click @keydown="text = text.slice(0, -1)">
        {{ '<' }}
      </Key>
      <Key class="absolute right-0 -bottom-13 w-12" @keydown="text += '\n'">
        {{ '__' }}
      </Key>
      <Key class="absolute left-32 -bottom-13 w-35" @keydown="text += ' '">
        {{ ' ' }}
      </Key>
    </div>
  </div>
</template>
