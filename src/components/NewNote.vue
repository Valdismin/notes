<template>
  <div class="new-note">
    <label>Title</label>
    <input type="text" v-model="note.title">
    <label>Description</label>
    <input type="text" v-model="note.description">
    <button class="btn btnPrimary" @click="addNote">Add Note</button>
  </div>
</template>

<script>
export default {
  name: "NewNote",
  data() {
    return {
      note: {
        title: "",
        description:"",
      }
    }
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note)
      this.note.title = ""
      this.note.description = ""
    }
  }
}
</script>

<style scoped>
.new-note {
  text-align: center;
  margin-bottom: 50px;
}
</style>
