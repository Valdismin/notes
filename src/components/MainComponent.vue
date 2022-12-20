<template>
  <div>
    <h1>{{title}}</h1>
    <new-note @addNote="addNote"/>
    <message-component v-show="message" :message="message"/>
    <div class="icons">
      <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
      <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
    </div>
    <notes-component :notes="notes" @removeNote="removeNote" :grid="grid"/>
  </div>
</template>

<script>
import MessageComponent from "@/components/MessageComponent";
import NewNote from "@/components/NewNote";
import NotesComponent from "@/components/NotesComponent";
export default {
  name: "MainComponent",
  components: {
    NotesComponent,
    NewNote,
    MessageComponent
  },
  data() {
    return {
      title: "NotesApp",
      grid: true,
      notes: [
        {
          id:1,
          title: "Note 1",
          description: "Description for 1 note",
          date: new Date(Date.now()).toLocaleString()
        },
        {
          id:2,
          title: "Note 2",
          description: "Description for 2 note",
          date: new Date(Date.now()).toLocaleString()
        },
        {
          id:3,
          title: "Note 3",
          description: "Description for 3 note",
          date: new Date(Date.now()).toLocaleString()
        },
      ],
      message: ""
    }
  },
  methods: {
    addNote (note) {
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
  }
}
</script>

<style lang="scss" scoped>
.icons {
  width: 100%;
  text-align: right;
  padding: 0 20px;

  svg {
    margin-right: 12px;
    color: #999999;
    &.active {
      color: #402caf;
    }
    &:last-child {
      margin-right: 0;
    }
  }
}
</style>
