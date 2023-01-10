<template>
  <div class="notes">
    <div class="note" :class="[{ full: !grid }, note.priority]" v-for="note in notes" :key="note.id">
      <note-component :note="note" :grid="grid" @removeNote="removeNote"/>
    </div>
  </div>
</template>

<script>

import NoteComponent from "@/components/NoteComponent";

export default {
  name: "NotesComponent",
  components: {NoteComponent},
  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    removeNote(id) {
      this.$emit('removeNote', id)
    }
  }
}
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}

.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #ffffff;
  transition: all .25s cubic-bezier(.02, .01, .47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, .02);

  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, .04);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }

  &.full {
    width: 100%;
    text-align: center;
  }

  &.standard {
    border: 1px solid green
  }
  &.middle {
    border: 1px solid yellow
  }
  &.high {
    border: 1px solid red
  }
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  h1 {
    font-size: 32px;
  }

  p {
    font-size: 22px;
    color: #402caf;
  }

  .icons {
    margin-right: 50px;

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


  &.full {
    justify-content: center;

    p {
      margin-right: 16px;

      &:last-child {
        margin-right: 0;
      }
    }
  }
}
</style>
