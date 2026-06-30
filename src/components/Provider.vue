<script setup lang="ts">
import type { ThemeMode } from '@/stores/app'
import { useDark } from '@vueuse/core'
import { computed, provide, ref, watch } from 'vue'
import { storeToRefs } from 'pinia'
import { BackTop } from '@/components/ui/back-top'
import { useAppStore } from '@/stores/app'

const appStore = useAppStore()
const { publicSettings } = storeToRefs(appStore)

const isScrolled = ref(false)
provide('isScrolled', isScrolled)

const themeMode = computed<ThemeMode>({
  get: () => appStore.themeMode,
  set: mode => appStore.updateThemeMode(mode),
})

useDark({
  storageKey: null,
  storageRef: themeMode,
  selector: 'html',
  attribute: 'class',
  valueDark: 'dark',
  valueLight: '',
  initialValue: 'auto',
})

watch(
  () => appStore.isDark,
  (dark) => {
    const root = document.documentElement
    if (dark)
      root.classList.add('dark')
    else
      root.classList.remove('dark')
    root.style.colorScheme = dark ? 'dark' : 'light'
  },
  { immediate: true },
)

watch(
  () => appStore.backgroundEnabled,
  (enabled) => {
    const body = document.body
    if (enabled)
      body.style.setProperty('background-color', 'transparent', 'important')
    else
      body.style.removeProperty('background-color')
  },
  { immediate: true },
)

// Theme selection from komari-theme-light
const themeSelection = computed(() => {
  const settings = publicSettings.value
  if (!settings?.theme_settings) return 'emerald'
  const themeSettings = settings.theme_settings as Record<string, unknown>
  const selection = themeSettings.themeSelection
  if (typeof selection === 'string') {
    return selection
  }
  return 'emerald'
})

watch(
  () => themeSelection.value,
  (newVal) => {
    const root = document.documentElement
    if (newVal && newVal !== 'emerald') {
      root.setAttribute('data-theme', newVal)
    } else {
      root.removeAttribute('data-theme')
    }
  },
  { immediate: true },
)
</script>

<template>
  <slot />
  <BackTop :visibility-height="1" @scrolled="isScrolled = $event" />
</template>