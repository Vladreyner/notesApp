<template>
  <div class="notes-list">
    <transition-group name="list" tag="div">
      <AppItem
        :note="note"
        :index="index"
        v-for="(note, index) in notes"
        :key="note"
        :activeNote="activeNote"
        @setActiveNote="setActiveNote"
      />
      <div class="notes-list-item block-disabled" v-if="!notes.length">No notes...</div>
    </transition-group>
  </div>
</template>

<script>
import AppItem from "./AppItem.vue";
export default {
  name: "AppList",
  components: {
    AppItem,
  },
  data() {
    return {
      note: "",
    };
  },
  props: {
    notes: {
      type: Array,
      default: () => [],
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
    setActiveNote(i) {
      this.$emit("setActiveNote", i);
    },
  },
  emits: {
    setActiveNote: null,
    saveNote: null,
    delNote: null,
    setEditMode: null,
  },
};
</script>

<style>
.notes-list {
  width: 20%;
  padding: 5px;
}

.block-disabled {
  background: #8080802e;
  cursor: default;
  color: #aaa8a8b3;
}
</style>
