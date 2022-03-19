<template>
  <div class="notes">
    <div
      class="note"
      :class="{ full: !grid }"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header">
        <p>{{ note.title }}</p>
        <button @click="removeNote(index)">&#215;</button>
      </div>

      <div class="note-body">
        <p>{{ note.desc }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },

    grid: {
      type: Boolean,
    },
  },

  methods: {
    removeNote(index) {
      this.$emit("removeNote", index);
    },
  },
};
</script>

<style lang="scss" scoped>
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
  background-color: #fff;
  transition: 0.3s;
  &:hover {
    transform: translate(0, -6px);
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
  }
  &.full {
    width: 100%;
    text-align: center;
  }
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  p {
    color: #402caf;
    font-size: 22px;
  }

  button {
    border: none;
    background: transparent;
    cursor: pointer;
    padding: 0;
    font-size: 27px;
  }
}

.note-body {
  p {
    margin: 20px 0;
  }

  span {
    font-style: 14px;
    color: #999;
  }
}
</style>