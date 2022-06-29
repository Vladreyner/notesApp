<template>

  <div
    :class="{
      'notes-list-item': true,
      active: index == activeNote,
    }"
    @click="setActiveNote(index)"
  >
    <div class="note-name">{{ note.title }}</div>
    <div class="note-date">{{ note.date }}</div>
  </div>

</template>

<script>
export default {
  name: "AppItem",
  props: {
    note: {
      type: Object,
      default: () => {},
    },
        activeNote: {
            type: Number,
            default: 0,
        },
        index: {
            type: Number,
            default: 0,
        }
  },
  methods: {
    setActiveNote(index) {
        this.$emit('setActiveNote', index);
    }
  },
  emits: {
    setActiveNote: null,
    saveNote: null,
    delNote: null,
    setEditMode: null,
  }
};
</script>

<style>
.note-name {
  white-space: nowrap;
  overflow-x: hidden;
  text-overflow: ellipsis;
}

.note-date {
  font-size: 11px;
}
.notes-list-item {
  width: 100%;
  display: block;
  border-radius: 10px;
  padding: 10px;
  background: gray;
  transition: linear;
  margin-top: 5px;
  cursor: pointer;
  color: #aaa8a8;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}

.list-leave-active {
  position: absolute;
  max-width: 170px;
}

.notes-list-item:first-child {
  margin-top: 0px;
}
.active {
  background: black;
  color: white;
  font-weight: bold;
}
</style>
