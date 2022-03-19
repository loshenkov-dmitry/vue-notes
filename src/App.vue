<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <message v-if="message" :message="message" />

          <newNote :note="note" @addNote="addNote" />
          <div class="notes-list-header">
            <h1>{{ title }}</h1>
            <search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />
            <div class="icons">
              <svg
                @click="grid = true"
                :class="{ active: grid }"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                @click="grid = false"
                :class="{ active: !grid }"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>

          <notes :notes="notesFilter" @removeNote="removeNote" :grid="grid" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message";
import newNote from "./components/NewNote";
import Notes from "./components/Notes.vue";
import search from "./components/Search.vue";
export default {
  data() {
    return {
      title: "Notes App",
      message: null,
      grid: true,
      search: "",
      note: {
        title: "",
        desc: " ",
      },
      notes: [
        {
          title: "First Note",
          desc: "Description of the first note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second Note",
          desc: "Description of the Second note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third Note",
          desc: "Description of the Third note",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },

  methods: {
    addNote() {
      let { title, desc } = this.note;

      if (title === "") {
        this.message = "Ошибка";
        return false;
      }

      this.notes.push({
        title,
        desc,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.message = null;
      this.note.title = "";
      this.note.desc = "";
    },

    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },

  computed: {
    notesFilter() {
      let array = this.notes;
      let search = this.search;

      if (!search) return array;

      search = search.trim().toLowerCase();

      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      return array;
    },
  },

  components: {
    message,
    newNote,
    Notes,
    search,
  },
};
</script>

<style lang="scss" scoped>
.notes-list-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  h1 {
    font-size: 32px;
  }

  svg {
    margin-right: 12px;
    color: #999;
    cursor: pointer;
    &:last-child {
      margin: 0;
    }
    &.active {
      color: #402caf;
    }
  }
}
</style>