<template>
  <input type="text" placeholder="todo" @keydown="press" v-model="value" />
</template>

<script>
export default {
  name: "todo-input",
  data: () => {
    return {
      value: ""
    };
  },
  methods: {
    press(e) {
      if (e.keyCode === 13) {
        this.$emit("todo-add", e.target.value);
        this.value = "";
      }
    }
  }
};
</script>


<style lang="scss" scoped>
input {
  width: 400px;
  height: 50px;
  border-radius: 30px;
  border: 1px solid rgba(0, 0, 0, 0.5);
  font-size: 2rem;
  padding: 10px 20px;
  box-sizing: border-box;
  outline: none;
}
</style>
