<template>
  <div id="todo-container">
    <Input @todo-add="add($event)" />
    <List
      :list="list"
      @todo-remove="remove($event)"
      @todo-toggle="toggle($event)"
      @todo-update="update($event)"
    />
  </div>
</template>

<script>
import Input from "./input.vue";
import List from "./list.vue";

export default {
  name: "todo-container",
  components: {
    Input,
    List
  },
  data: () => {
    return {
      list: []
    };
  },
  methods: {
    add(text) {
      const id = this.list.length + 1;
      this.list.push({ id, text, complete: false });
    },
    toggle(index) {
      this.list[index].complete = !this.list[index].complete;
    },
    remove(id) {
      this.list = this.list.filter(element => element.id !== id);
    },
    update(item) {
      const index = this.list.findIndex(element => element.id === item.id);
      this.list[index] = { id: item.id, text: item.text, complete: false };
    }
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
ul {
  list-style: none;
}

#todo-container {
  margin: auto;
  font-size: 2rem;
}
</style>