<template>
  <div id="Wrapper">
    <div id="TaskTitleWrapper">
      <span>Add a new task</span>
    </div>
    <div id="TaskInputWrapper" @keyup.enter="$emit('create-new-task', task)">
      <input
        type="text"
        placeholder="Enter a task name"
        v-model="task.newTaskTitle"
      />
      <input
        type="text"
        placeholder="Enter a task description"
        v-model="task.newTaskDesc"
      />
      <button @click="$emit('create-new-task', task)">+</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NewTask",
  components: "",
  props: {},
  data() {
    return {
      task: {
        newTaskTitle: "",
        newTaskDesc: "",
      },
    };
  },
  methods: {},
  computed: {},
};
</script>

<style>
#Wrapper {
  background-color: white;
  margin: 10px auto;
}

#TaskTitleWrapper {
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

#TaskTitleWrapper span {
  font-size: 36px;
  font-weight: 600;
}

#TaskInputWrapper {
  display: flex;
  justify-content: center;
  align-items: center;

  gap: 5vw;
}

#TaskInputWrapper button {
  padding: 10px;
  border: none;

  background-color: black;
  color: white;
  cursor: pointer;

  will-change: background-color;
  transition: 0.2s ease;
}

#TaskInputWrapper button:active {
  background-color: #3a3a3a;
}

input {
  border: none;
  font-size: 16px;

  line-height: 16px;
  height: 20px;

  background-color: #f4f4f4;
  padding: 10px 5px;
  outline: none;
}

input:focus,
input:active {
  color: black;
  outline: #f4f4f4;
}
</style>
