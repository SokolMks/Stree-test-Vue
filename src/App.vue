<template>
  <div id="app">
    <vHeader v-model="search"></vHeader>
    <BookLibrary :search="search" />
  </div>
</template>

<script>
import vHeader from "./components/Header";
import BookLibrary from "./components/BookLibrary";
export default {
  data() {
    return {
      search: ""
    };
  },
  name: "app",
  components: {
    vHeader,
    BookLibrary
  },
  methods: {}
};
</script>

<style>
#app {
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0px;
  padding: 0px;
}
</style>