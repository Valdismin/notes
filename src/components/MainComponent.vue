<template>
  <div>
    <h1>{{title}}</h1>
    <div class="new-note">
      <input type="text" v-model="newNote.title">
      <input type="text" v-model="newNote.description">
      <button @click="addNote">Add Note</button>
      <div v-show="message">
        {{message}}
      </div>
    </div>
    <div class="notes">
      <div class="note" v-for="(note, index) in notes" :key="index">
        <div class="node-header">
          <p>{{note.title}}</p>
        </div>
        <div class="note-body">
          <p>{{note.description}}</p>
          <span>{{note.date}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainComponent",
  data() {
    return {
      title: "Notes",
      notes: [
        {
          title: "Note 1",
          description: "Description for 1 note",
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: "Note 2",
          description: "Description for 2 note",
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: "Note 3",
          description: "Description for 3 note",
          date: new Date(Date.now()).toLocaleString()
        },
      ],
      newNote: {
        title:"",
        description:""
      },
      message: ""
    }
  },
  methods: {
    addNote () {
      let {title, description} = this.newNote

      if (title === "") {
        this.message = "title can't be blank"
        return false
      }

      if (description === "") {
        this.message = "description can't be blank"
        return false
      }

      this.notes.push({
        title,
        description,
        date: new Date(Date.now()).toLocaleString()
      })

      this.newNote.title = ""
      this.newNote.description = ""
      this.message = ""
    }
  }
}
</script>

<style scoped>

</style>
