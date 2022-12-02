<template>
  <div class="hello">
    <div class="filter-bar">
      <button @click="filterBy = 'all'">all</button>
      <button @click="filterBy = 'todo'">todo</button>
      <button @click="filterBy = 'done'">done</button>
    </div>
    <new-task @create-new-task="createNewTask" />
    <div class="taskWrapper">
      <div class="tasks" v-for="task in tasksToShow" :key="task.taskId">
        <task-item
          class="blue"
          :task-details="task"
          @task-update="updateATask"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./TaskItem";
import NewTask from "./NewTask";
export default {
  name: "TodoList",
  components: { NewTask, TaskItem },
  data() {
    return {
      tasks: [],
      filterBy: "all",
    };
  },
  mounted() {
    this.getFromLocalStorage();
  },
  methods: {
    createNewTask(task) {
      // adds a new task to the array
      let newTask = {
        taskTitle: task.newTaskTitle,
        taskDescription: task.newTaskDesc,
        taskStatus: "todo",
        taskId: this.newTaskId,
      };
      if (newTask.taskTitle.length > 0 && newTask.taskDescription.length > 0) {
        this.tasks.push(newTask);
        this.saveToLocalStorage();
      } else {
        alert("You need to fill name and description");
      }
    },
    updateATask(upTask) {
      this.tasks.forEach((task) => {
        if (task.taskId === upTask.itemId) {
          task.taskTitle = upTask.itemTitle;
          task.taskDescription = upTask.itemDesc;
          task.taskStatus = upTask.itemStatus;
        }
      });
      this.saveToLocalStorage();
    },
    getFromLocalStorage() {
      if (localStorage.tasks)
        this.tasks = JSON.parse(localStorage.getItem("tasks"));
    },
    saveToLocalStorage() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
  computed: {
    newTaskId() {
      return (
        this.tasks.reduce((max, curr) => Math.max(max, curr.taskId), 0) + 1
      );
    },
    tasksToShow() {
      return this.filterBy === "all"
        ? this.tasks.filter((task) => task.taskStatus !== "deleted")
        : this.tasks.filter((task) => task.taskStatus === this.filterBy);
    },
  },
};
</script>

<style scoped>
.hello {
  min-width: 50vw;
}
.blue {
  background-color: #fdfdfd;
}
.filter-bar {
  display: flex;
  justify-content: space-around;
  gap: 10vw;
  border-radius: 10px;
  padding-bottom: 10px;
}

.filter-bar button {
  padding: 5px 25px;
  border-radius: 10px;

  background-color: black;
  color: whitesmoke;
  border: none;

  cursor: pointer;
  font-size: 20px;
  font-weight: 500;
  line-height: 1.5;

  transition: 0.2s ease;
}

.filter-bar button:hover {
  background-color: #3a3a3a;
}

.taskWrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  gap: 40px;
}

.tasks {
  min-width: 600px;
  padding: 0 30px;
}
</style>
