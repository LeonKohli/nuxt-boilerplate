<template>
  <Button
    variant="ghost"
    size="icon"
    :aria-label="label"
    @click="toggle"
    class="transition-all duration-200 hover:scale-105"
  >
    <Icon :name="icon" class="w-5 h-5 transition-all duration-300 ease-in-out" />
  </Button>
</template>

<script setup lang="ts">
const colorMode = useColorMode()

const isDarkMode = computed(() => colorMode.value === 'dark')
const icon = computed(() => isDarkMode.value ? 'lucide:moon' : 'lucide:sun')
const label = computed(() => isDarkMode.value ? 'Switch to light mode' : 'Switch to dark mode')

function toggle() {
  const isSystemPreference = colorMode.preference === 'system'
  const targetMode = isDarkMode.value ? 'light' : 'dark'
  
  colorMode.preference = targetMode
}
</script>
