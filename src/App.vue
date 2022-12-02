<template>
  <div id="app">
    <div id="Title">
      <span>TODO List!</span>
    </div>
    <todo-list />
  </div>
</template>

<script>
import TodoList from "./components/TodoList";
export default {
  name: "app",
  components: {
    TodoList,
  },
};
</script>

<style>
#app {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 5px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  user-select: none;
}
#app #Title span {
  display: block;
  padding: 20px;
  font-size: 40px;

  background-color: black;
  color: white;
  border-radius: 20px;

  margin-bottom: 30px;
}
</style>
