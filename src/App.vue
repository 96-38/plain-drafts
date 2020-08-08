<template>
  <div id="todo" lang="html">
    <input v-model="todo" />
    <div>{{ todo }}</div>
    <div id="app">hello vue</div>
    <button v-on:click="add()">add</button>
    <ul v-for="(item, id) in todoList" v-bind:key="id">
      <list-item v-bind:contents="item" v-bind:remove="() => remove(id)" />
    </ul>
    <ListItem contents="example" />
  </div>
</template>

<style scoped>
#app {
  font-size: 2em;
  text-align: center;
}
</style>

<script>
import Vue from "vue";
import ListItem from "./ListItem";

export default Vue.extend({
  data() {
    return {
      todo: "",
      todoList: [],
    };
  },
  methods: {
    add() {
      this.todoList.push(this.todo);
      this.todo = "";
    },
    remove(id) {
      this.todoList.splice(id, 1);
    },
  },
  components: {
    ListItem,
  },
});
</script>
