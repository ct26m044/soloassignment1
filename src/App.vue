<script setup>
import { ref } from 'vue'
import { useNotes } from './composables/useNotes.js'
import NoteForm from './components/NoteForm.vue'
import NoteCard from './components/NoteCard.vue'
import SearchBar from './components/SearchBar.vue'

const { addNote, deleteNote, filteredNotes } = useNotes()

const searchTerm = ref('')
const visibleNotes = filteredNotes(searchTerm)
</script>

<template>
  <h1>Notes</h1>

  <NoteForm @add="addNote" />
  <SearchBar v-model="searchTerm" />

  <NoteCard v-for="note in visibleNotes"
    :key="note.id"
    :note="note"
    @delete="deleteNote"
  />
</template>