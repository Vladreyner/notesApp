<template>
  <div class="site-witdh">
    <AppList
      :notes="notes"
      :activeNote="activeNote"
      @set-active-note="setActiveNote"
    />
    <AppNote
      :activeNote="activeNote"
      :activeNoteTitle="activeNoteTitle"
      :activeNoteText="activeNoteText"
      :editMode="editMode"
      @newNoteLocal="newNoteLocal"
    />
  </div>
</template>

<script>
import AppNote from "./Notes/AppNote.vue";
import AppList from "./Notes/AppList.vue";

export default {
  components: {
    AppNote,
    AppList,
  },
  data() {},
  props: {
    notes: {
      type: Array,
      default: () => [],
    },
    activeNote: {
      type: String,
      default: "none",
    },
    activeNoteTitle: {
      type: String,
      default: "",
    },
    activeNoteText: {
      type: String,
      default: "",
    },
    editMode: {
      type: Boolean,
      default: false,
    },
    data: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    setActiveNote(i) {
      this.$emit("setActiveNote", i);
    },
    newNoteLocal(data) {
      this.$emit("newNoteLocal", {
        title: data.title,
        text: data.text,
        date: data.date,
      });
    },
  },
  emits: {
    setActiveNote: null,
    saveNote: null,
    delNote: null,
    setEditMode: null,
    newNoteLocal: null,
  },
};
</script>

<style scoped></style>
