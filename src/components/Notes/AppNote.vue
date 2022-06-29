<template>
  <div class="note-data">
    <transition name="fade">
      <div v-if="activeNote !== 'none'">
        <div class="note-body" v-if="!editMode">
          <h1>
            <span class="low-visible">title:</span>
            {{ activeNoteTitle }}
          </h1>
          <span class="low-visible" @click="test()">text: </span
          >{{ activeNoteText }}
        </div>

        <div class="note-body" v-else>
          <h2>
            <span class="low-visible">title: </span>
            <input type="text" v-model="newNoteLocal.title" />
          </h2>
          <span class="low-visible" @click="test">text: </span>
          <textarea rows="5" cols="33" v-model="newNoteLocal.text"></textarea>
          <br /><br />
          <button @click="newNote(this.newNoteLocal)">Save</button>
        </div>
      </div>
      <!-- <div v-else>Choose one</div> -->
    </transition>
  </div>
</template>

<script>
export default {
  name: "AppNote",
  data() {
    return {
      newNoteLocal: {
        title: this.activeNoteTitle ?? "",
        text: this.activeNoteText ?? "",
        date: this.createDate(),
      },
    };
  },
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
      this.$emit("newNoteLocal", {
        title: this.newNoteLocal.title,
        text: this.newNoteLocal.text,
        date: this.newNoteLocal.date,
      });
    },
    createDate() {
      let date = new Date();
      let createDateNow =
        String(date.getDate()).padStart(2, "0") +
        "." +
        String(date.getMonth() + 1).padStart(2, "0") +
        "." +
        date.getFullYear();
      return createDateNow;
    },
  },
  watch: {
    activeNoteTitle: {
      handler(data) {
        this.newNoteLocal.title = data;
      },
    },
    activeNoteText: {
      handler(data) {
        this.newNoteLocal.text = data;
      },
    },
  },
  emits: {
    newNoteLocal: null,
  },
};
</script>

<style scoped>
.note-data {
  width: 80%;
}

.note-body {
  background-color: gray;
  color: white;
  border-radius: 10px;
  padding: 10px;
  margin: 5px;
}

span.low-visible {
  color: #999;
  font-size: 17px;
}

textarea {
  border: none;
  border-radius: 10px;
  padding: 10px;
  margin-top: 5px;
}

input {
  border: none;
  border-radius: 10px;
  padding: 10px;
}

/* Vue 3 anims */

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
