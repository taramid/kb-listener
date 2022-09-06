<script setup lang="ts">

import {ref} from 'vue'

import Keyboard from '@/components/Keyboard.vue'

const val = ref<number | null>(null)

</script>

<template>

  <div>

    <h1>{{ val }}</h1>

    <Keyboard v-model="val"/>

  </div>

</template>
