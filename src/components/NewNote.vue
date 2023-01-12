<template>
  <div class="new-note">
    <label>Title</label>
    <input type="text" v-model="note.title">
    <h5>Priority</h5>
    <div class="radio-buttons">
      <div>
        <label>Standard</label>
        <input type="radio" value="standard" v-model="note.priority"/>
      </div>
      <div>
        <label>Middle</label>
        <input type="radio" value="middle" v-model="note.priority"/>
      </div>
      <div>
        <label>High</label>
        <input type="radio" value="high" v-model="note.priority"/>
      </div>
    </div>
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
        description: "",
        priority:"standard"
      }
    }
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note)
      this.note.title = ""
      this.note.description = ""
      this.note.priority = "standard"
    }
  }
}
</script>

<style lang="scss" scoped>
.new-note {
  text-align: center;
  margin-bottom: 50px;
  .radio-buttons{
    display: flex;
    justify-content: center;
    margin: 20px auto;
    div {
      margin: 0 20px;
    }
  }
}
</style>
