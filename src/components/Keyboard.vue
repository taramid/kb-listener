<script setup lang="ts">

import {ref, computed} from 'vue'
import {useEventListener} from '@vueuse/core'

import {Arabic} from "@/types"

const props = defineProps<{
  modelValue: number | null,
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: number | null): void
  (e: 'submit', value: number): void
}>()

const
    digits = ref<Array<Arabic>>([]),
    answer = computed<number | null>(() => parseInt(digits.value.join(''), 10) || null)

const cleanup = useEventListener(document, 'keydown', (e) => {

  if (['Enter', 'NumpadEnter'].includes(e.code)) {

    if (answer.value) {
      emit('submit', answer.value as number)
      digits.value = []
    }

  } else if (['Backspace', 'Delete'].includes(e.code)) {

    digits.value.pop()
    emit('update:modelValue', answer.value)

  } else {
    const digit = parseInt(e.key, 10)
    if ((Object.values(Arabic)).includes(digit)) {

      digits.value.push(digit)
      emit('update:modelValue', answer.value)
    }
  }
})

</script>

<template></template>
