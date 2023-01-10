<template>
  <div>
    <new-note @addNote="addNote"/>
    <message-component v-show="message" :message="message"/>
    <div class="note-header">
      <h1>{{ title }}</h1>
      <search-component placeholder="Find your search" @search="search = $event"/>
      <div class="icons">
        <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg"
             width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
             stroke-linecap="round" stroke-linejoin="round">
          <rect x="3" y="3" width="7" height="7"></rect>
          <rect x="14" y="3" width="7" height="7"></rect>
          <rect x="14" y="14" width="7" height="7"></rect>
          <rect x="3" y="14" width="7" height="7"></rect>
        </svg>
        <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer;"
             xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
             stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="8" y1="6" x2="21" y2="6"></line>
          <line x1="8" y1="12" x2="21" y2="12"></line>
          <line x1="8" y1="18" x2="21" y2="18"></line>
          <line x1="3" y1="6" x2="3" y2="6"></line>
          <line x1="3" y1="12" x2="3" y2="12"></line>
          <line x1="3" y1="18" x2="3" y2="18"></line>
        </svg>
      </div>
    </div>
    <notes-component :notes="searchNotes" @removeNote="removeNote" :grid="grid"/>
  </div>
</template>

<script>
import MessageComponent from "@/components/MessageComponent";
import NewNote from "@/components/NewNote";
import NotesComponent from "@/components/NotesComponent";
import SearchComponent from "@/components/SearchComponent";

export default {
  name: "MainComponent",
  components: {
    SearchComponent,
    NotesComponent,
    NewNote,
    MessageComponent
  },
  data() {
    return {
      title: "NotesApp",
      grid: true,
      search:"",
      notes: [
        {
          id: 1,
          title: "Note 1",
          description: "Description for 1 note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "standard"
        },
        {
          id: 2,
          title: "Note 2",
          description: "Description for 2 note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "middle"
        },
        {
          id: 3,
          title: "Note 3",
          description: "Description for 3 note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "high"
        },
      ],
      message: ""
    }
  },
  methods: {
    addNote(note) {
      let {title, description} = note

      if (title === "") {
        this.message = "title can't be blank"
        return false
      }

      if (description === "") {
        this.message = "description can't be blank"
        return false
      }

      this.notes.push({
        id: Math.floor(Math.random() * 100000),
        title,
        description,
        date: new Date(Date.now()).toLocaleString()
      })

      this.message = ""
    },
    removeNote(id) {
      this.notes = this.notes.filter(note => note.id !== id)
    }
  },
  computed: {
    searchNotes() {
      return this.notes.filter(note => note.title.toLowerCase().includes(this.search.trim().toLowerCase()))
    }
  }
}
</script>

<style lang="scss">
.icons {
  display: flex;
  margin-top: 50px;
  margin-left: 100px;
}
</style>
