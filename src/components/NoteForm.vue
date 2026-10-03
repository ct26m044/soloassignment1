<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add'])

const title = ref('')
const content = ref('')
const tagsText = ref('')

function submit() {
  if (!title.value) return

  const tags = tagsText.value.split(',').map(tag => tag.trim()).filter(tag => tag !== '')

  emit('add', { title: title.value, content: content.value, tags: tags })

  title.value = ''
  content.value = ''
  tagsText.value = ''
}
</script>

<template>
  <div>
    <input v-model="title" placeholder="Title">
    <textarea v-model="content" placeholder="Content"></textarea>
    <input v-model="tagsText" placeholder="Tags">
    <button @click="submit">Save Note</button>
  </div>
</template>