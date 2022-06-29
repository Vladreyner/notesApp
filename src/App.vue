<template>
  <div>
    <AppHeader
      :editMode="editMode"
      :activeNote="activeNote"
      @newNote="newNote"
      @saveNote="saveNote"
      @delNote="delNote"
      @setEditMode="setEditMode"
    />
    <AppMain
      :notes="notes"
      :activeNote="activeNote"
      :activeNoteTitle="activeNoteTitle"
      :activeNoteText="activeNoteText"
      :editMode="editMode"
      @set-active-note="setActiveNote"
      @newNoteLocal="saveNote"
    />
  </div>
</template>

<script>
import AppHeader from "./components/layouts/Header/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

export default {
  components: {
    AppHeader,
    AppMain,
  },
  data() {
    return {
      notes: [],
      activeNote: "none",
      activeNoteTitle: "",
      activeNoteText: "",
      activeNoteDate: "",
      editMode: false,
    };
  },
  methods: {
    newNote() {
      let date = new Date();
      let createDate =
        String(date.getDate()).padStart(2, "0") +
        "." +
        String(date.getMonth() + 1).padStart(2, "0") +
        "." +
        date.getFullYear();
      let noteTitle = "New note #" + (this.notes.length + 1);
      let localNote = {
        title: noteTitle,
        text: "Your",
        date: createDate,
      };
      this.notes.unshift(localNote);
      if (this.activeNote !== "none") {
        this.activeNote = this.activeNote + 1;
      } else {
        this.setActiveNote(0);
      }
      this.setLocal();
    },
    delNote() {
      if (this.activeNote !== "none") {
        this.notes.splice(this.activeNote, 1);
        this.activeNote = "none";
        this.setLocal();
      }
    },
            saveNote(data) {
            this.editMode = false;
            this.notes.splice(this.activeNote, 1);
            this.notes.unshift(data);
            this.setActiveNote(0);
            this.setLocal();
        },
            setEditMode() {
            if (this.activeNote !== 'none') {
            this.editMode = true;
            console.log('true');
            } else {
                console.log('Choose a note to edit')
            }
        },
    setActiveNote(i) {
      this.activeNote = i;
      this.activeNoteTitle = this.notes[i].title;
      this.activeNoteText = this.notes[i].text;
      this.activeNoteDate = this.notes[i].date;
    },
    setLocal() {
      localStorage.setItem("notesArray", JSON.stringify(this.notes));
    },
  },

  mounted() {
    const getLocal = JSON.parse(localStorage.getItem("notesArray"));
    if (getLocal !== null) {
      this.notes = getLocal;
    } else {
      this.setLocal();
    }
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap");

* {
  font-family: Inter, Roboto, Oxygen, Fira Sans, Helvetica Neue, sans-serif;
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0px;
  font-size: 20px;
  display: border-box;
}

body {
  background: #575757;
}

[v-cloak] {
  display: none;
}

.width50 {
  width: 50%;
}

.site-witdh {
  display: flex;
  max-width: 900px;
  text-align: left;
  margin: 0 auto;
}

.text-right {
  text-align: right;
}

.text-left {
  text-align: left;
}

.notes-list-item {
  transition: all 0.5s ease;
  margin-right: 10px;
}
</style>
