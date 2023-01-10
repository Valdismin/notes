<template>
  <div>
    <div class="note-header" :class="{ full: !grid }">
      <p v-if="!isEdit.header" @dblclick="editHeader">{{ noteValues.header }}</p>
      <input ref="header" v-else v-model="noteValues.header" autofocus @keyup="activateViewModeHeader" @blur="activateViewModeHeader"/>
      <div style="cursor: pointer" @click="removeNote(note.id)">X</div>
    </div>
    <div class="note-body">
      <p v-if="!isEdit.description" @dblclick="editDescription">{{ noteValues.description }}</p>
      <input ref="description" v-else v-model="noteValues.description" autofocus @keyup="activateViewModeDescription" @blur="activateViewModeDescription"/>
      <span>{{ date }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "NoteComponent",
  props: {
    note: {
      type: Object,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      isEdit: {
        header: false,
        description: false
      },
      noteValues: {
        description: this.note.description,
        header: this.note.title,
        initialDescription: "",
        initialHeader: ""
      },
      date: this.note.date
    }
  },
  methods: {
    removeNote(id) {
      this.$emit('removeNote', id)
    },
    editHeader () {
      this.noteValues.initialHeader = this.noteValues.header
      this.isEdit.header = true
      this.$nextTick(() => this.$refs.header.focus())
    },
    editDescription () {
      this.noteValues.initialDescription = this.noteValues.description
      this.isEdit.description = true
      this.$nextTick(() => this.$refs.description.focus())
    },
    activateViewModeHeader($event) {
      if($event.key === "Enter" || $event.type === "blur") {
        this.isEdit.header = false
        this.date = new Date(Date.now()).toLocaleString()
      } else if ($event.key === "Escape") {
        this.noteValues.header = this.noteValues.initialHeader
        this.isEdit.header = false
      }
    },
    activateViewModeDescription($event) {
      if($event.key === "Enter" || $event.type === "blur") {
        this.isEdit.description = false
        this.date = new Date(Date.now()).toLocaleString()
      } else if ($event.key === "Escape") {
        this.noteValues.description = this.noteValues.initialDescription
        this.isEdit.description = false
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.note-body {
  display: flex;
  flex-direction: column;
  p {
    margin: 20px 0;
  }

  span {
    font-size: 14px;
    color: #999999;
  }
  input {
    margin: 20px 0;
  }
}
input {
  max-width: 400px;
  margin-bottom: 0;
}
</style>
