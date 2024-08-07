<template>
    <button @click="toggleMode" class="hover:bg-gray-200 dark:hover:bg-gray-600 px-2 py-1 text-gray-500">{{ nextModeIcon }}</button>
</template>

<script setup lang="ts">
const colorMode = useColorMode();

const modes = [
    'system',
    'light',
    'dark'
]

const nextModeIcons = {
  system: '🌓',
  light: '🌕',
  dark: '🌑'
}


const nextMode = computed(() => {
    const currentModeIndex = modes.indexOf(colorMode.preference);
    let nextModeIndex = null;

    if(currentModeIndex === modes.length - 1) {
        nextModeIndex = 0;
    } else {
        nextModeIndex = currentModeIndex + 1;   
    }

    return modes[nextModeIndex]
})

const nextModeIcon = computed(() => nextModeIcons[nextMode.value as keyof typeof nextModeIcons])

const toggleMode = () => colorMode.preference = nextMode.value as string;
</script>