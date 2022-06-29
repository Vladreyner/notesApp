<template>
  <header>
    <div class="site-witdh">
      <div class="width50 text-left">
        <h2>notesApp</h2>
      </div>
      <div class="width50 text-right">
        <button
          :class="{
            hidden: activeNote == 'none',
          }"
          @click="delNote"
        >
          Delete
        </button>
        <button
          :class="{
            hidden: activeNote == 'none',
            hidden: editMode == true,
          }"
          @click="setEditMode"
        >
          Edit
        </button>
        <button
          :class="{
            hidden: editMode === true,
          }"
          @click="newNote"
        >
          New
        </button>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
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
  },
  methods: {
    newNote() {
      this.$emit("newNote");
    },
    saveNote() {
      this.$emit("saveNote");
    },
    delNote() {
      this.$emit("delNote");
    },
    setEditMode() {
      this.$emit("setEditMode");
    },
  },
  emits: {
    newNote: null,
    saveNote: null,
    delNote: null,
    setEditMode: null,
  },
};
</script>

<style scoped>

header {
  color: white;
  background: #2f2f2f;
  padding: 10px;
}
.hidden {
  display: none;
}

button {
  border: none;
  color: white;
  margin-right: 10px;
  border-radius: 5px;
  font-size: 15px;
  padding: 5px;
  background-color: gray;
  cursor: pointer;
  transition: linear;
}

button:hover {
  color: black;
  background: white;
}

button:active {
  background-color: black;
}
</style>
