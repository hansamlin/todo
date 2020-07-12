<template>
  <ul>
    <li v-for="(item, index) in list" :key="index">
      <input
        type="text"
        v-model="value"
        v-if="update.id === item.id && update.active === true"
        @keydown="press"
        id="update-input"
      />

      <span
        :class="{ complete: item.complete }"
        @click="click(item.id)"
        v-if="update.id !== item.id"
      >{{ item.text }}</span>
      <button @click="toggle(index)" v-if="update.id !== item.id">v</button>
      <button @click="remove(item.id)" v-if="update.id !== item.id">x</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "todo-list",
  props: {
    list: {
      type: Array,
      required: true
    }
  },
  data: () => {
    return {
      update: { active: false, id: 0 },
      value: ""
    };
  },
  methods: {
    remove(id) {
      this.$emit("todo-remove", id);
    },
    toggle(id) {
      this.$emit("todo-toggle", id);
    },
    click(id) {
      this.update = { active: true, id };
      this.value = this.list.find(element => element.id === id).text;
    },
    press(e) {
      if (e.keyCode === 13) {
        this.$emit("todo-update", { id: this.update.id, text: this.value });
        this.reset();
      }

      if (e.keyCode === 27) {
        this.reset();
      }
    },
    reset() {
      this.update = { active: false, id: 0 };
    }
  },
  updated() {
    if (this.update.active === true && this.update.id !== 0) {
      document.getElementById("update-input").focus();
    }
  }
};
</script>

<style lang="scss" scoped>
ul {
  width: 400px;
  margin: 1rem 0 0 0;
  background-color: lightcoral;
  border-radius: 30px;

  li {
    height: 50px;
    border-radius: 30px;
    text-align: left;
    padding: 0 20px;
    box-sizing: border-box;
    display: flex;
    position: relative;
    line-height: 50px;
    animation: fadeIn 1s forwards;

    @keyframes fadeIn {
      from {
        opacity: 0;
      }

      to {
        opacity: 1;
      }
    }

    input {
      width: 100%;
      font-size: 2rem;
      border: none;
      height: 80%;
      margin: auto;
      padding: 0 10px;
    }

    span {
      flex: 8;
      cursor: pointer;
    }

    .complete {
      text-decoration: line-through;
    }

    button {
      font-size: 1.125rem;
      cursor: pointer;
      background-color: transparent;
      border: none;
      outline: none;
      transition: background-color 0.5s;
      border-radius: 6px;
      flex: 1;
      margin: 5px;
    }
  }
}
</style>