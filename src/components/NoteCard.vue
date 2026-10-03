<script setup lang="ts">
import BaseCard from './BaseCard.vue'
import type { Note } from '../types/note.ts'

defineProps<{ note: Note }>()
defineEmits(['delete'])
</script>

<template>
  <BaseCard>
    <template #header>
      <strong>{{ note.title }}</strong>
    </template>

    <p>{{ note.content }}</p>
    <small>Tags: {{ note.tags.join(', ') }}</small>
    <br>
    <button @click="$emit('delete', note.id)">Delete</button>
  </BaseCard>
</template>