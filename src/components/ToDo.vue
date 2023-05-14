<template>
  <li>
    <div class="toDoTitleBox">
      <h4>Lista todo</h4>
      <p>Wykonane: {{ done }}</p>
    </div>
    <ul>
      <li
        @click="handleDone"
        class="toDoItem"
        v-for="toDo in toDoList"
        :key="toDo.id"
        :class="{
          inActive: !toDo.done,
        }"
        :value="toDo.done"
        :data-id="toDo.id"
      >
        <CheckIcon class="icon" v-if="toDo.done" />
        <p>{{ toDo.text }}</p>
      </li>
      <li class="toDoAdd">
        <form @submit="handleInput">
          <input
            ref="input"
            name="toDo"
            class="toDoInput"
            type="text"
            v-model="newToDo"
            placeholder="+ Dodaj nowy element checklisty"
          />
        </form>
      </li>
    </ul>
  </li>
</template>

<script>
import CheckIcon from "./CheckIcon.vue";

export default {
  components: {
    CheckIcon,
  },
  data() {
    return {
      newToDo: "",
      toDoList: [
        { text: "Lorem ipsum dolor sit amet, consectetur", done: true, id: 1 },
        { text: "Sed do eiusmod tempo incididunt ", done: false, id: 2 },
        { text: "Labore et doore manga aliqa", done: false, id: 3 },
        {
          text: "Sed ut perspiciatis nde omnis iste nauts",
          done: false,
          id: 4,
        },
        {
          text: "Minia venima, quis nostrum exercitationem",
          done: false,
          id: 5,
        },
      ],
    };
  },

  computed: {
    done() {
      const doneToDo = this.toDoList.filter(ele => ele.done)?.length;
      return doneToDo;
    },
  },

  methods: {
    handleDone(event) {
      event.preventDefault();
      if (!event.currentTarget?.dataset.id) return;

      const toDoID = event.currentTarget.dataset.id;
      const toDoDone = this.toDoList[toDoID - 1].done;
      this.toDoList[toDoID - 1].done = !toDoDone;
    },

    handleInput(event) {
      event.preventDefault();
      const { value } = event.currentTarget.elements.toDo;
      console.log(value);
      if (value === "") return;
      this.toDoList.push({
        text: value,
        done: false,
      });
      this.$refs.input.blur();
      this.newToDo = "";
    },
  },
};
</script>

<style scoped>
.toDoTitleBox {
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  color: var(--var-title-color);
  font-weight: 700;
}
.toDoItem {
  position: relative;
  font-size: 12px;
  padding-top: 10px;
  padding-bottom: 8px;
  padding-left: 25px;
  border-bottom: 0.5px var(--var-btn-border-color) solid;
  cursor: pointer;
}
.toDoItem:hover {
  background-color: var(--var-bg);
}

.toDoAdd {
  font-size: 12px;
  padding-top: 10px;
  padding-bottom: 8px;
  padding-left: 5px;
  border-bottom: 0.5px var(--var-btn-border-color) solid;
  cursor: pointer;
}

.toDoInput {
  width: 100%;
  font-size: 12px;
  color: var(--var-txt-color);
  border: none;
  outline: none;
}

.inActive::before {
  position: absolute;
  display: inline;
  content: "";
  left: 5px;
  width: 10px;
  height: 10px;
  border-radius: 50px;
  border: 1px var(--var-btn-border-color) solid;
}

.icon {
  position: absolute;
  display: inline-block;
  left: 5px;
  width: 15px;
  height: 15px;
  fill: var(--var-btn-color);
}
.toDoAdd:has(.toDoInput:focus) {
  border-bottom: 2px var(--var-btn-color) solid;
}
</style>
