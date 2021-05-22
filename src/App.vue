<template>
  <div class="card">
    <h1
      :style="{
        color: inputValue.length < 5 ? 'darkred' : 'darkblue',
        fontSize: inputValue.length < 6 ? '2rem' : '1.5rem',
      }"
    >
      {{ title }}
    </h1>
    <div class="form-control">
      <input
        type="text"
        :placeholder="placeholderString"
        v-model="inputValue"
        @keypress.enter="addNewNote"
      />
    </div>
    <h2>inputValue: {{ inputValue }}</h2>
    <button class="btn" @click="addNewNote">Добавить</button>
    <hr />
    <ul class="list" v-if="notes.length !== 0">
      <li class="list-item" v-bind:key="note" v-for="(note, index) in notes">
          <!--<span :class="note.length > 5 ? 'primary' : 'bold'">({{ index }}){{ toUpperCase(note) }}</span> -->
          
          <!--<span :class="{
            'primary' : true,
            'bold' : note.length > 5
          }">({{ index }}){{ toUpperCase(note) }}</span>-->

          <span :class="['bold', {'primary': note.length > 5}]">({{ index }}){{ toUpperCase(note) }}</span>

        <button class="btn danger" @click="removeNote(index)">удалить</button>
      </li>
      <hr />
      <li>
        <strong>Общее количество : {{ notes.length }}</strong> | Удвоенное:
        {{ doubleCountComputed }}
      </li>
    </ul>
    <div v-else>Заметок пока нет. Добавьте первую</div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      title: "Список заметок",
      placeholderString: "Введите название заметки",
      inputValue: "",
      notes: ["Заметка 1", "Заметка 2"],
    };
  },
  methods: {
    addNewNote() {
      if (this.inputValue != "") {
        this.notes.push(this.inputValue);
        this.inputValue = "";
      }
    },
    toUpperCase(item) {
      return item.toUpperCase();
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
    doubleCount() {
      return this.notes.length * 2;
    },
  },
  computed: {
    doubleCountComputed() {
      return this.notes.length * 2;
    },
  },
  watch: {
    inputValue(value) {
      if (value.length > 10) {
        this.inputValue = "";
      }
    },
  },
};
</script>

<style lang="scss">
@import "./assets/theme.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
