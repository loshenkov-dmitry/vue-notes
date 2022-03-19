<template>
  <div class="new-note">
    <label>Title</label>
    <input v-model="note.title" type="text" />
    <label>Description</label>
    <textarea v-model="note.desc"></textarea>
    <button class="btn btnPrimary" @click="addNote">New Note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: Object,
  },

  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    },
  },
};
</script>

<style lang="scss" scoped>
.new-note {
  text-align: center;
}
button {
  margin: 20px 0;
}
</style>