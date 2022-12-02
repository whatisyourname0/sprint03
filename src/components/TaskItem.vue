<template>
  <div id="wrapper">
    <div>
      <div>
        <div class="clickable" @click="showDescription = !showDescription">
          <input
            class="clickable"
            :disabled="!editTitle"
            type="text"
            v-model="task.itemTitle"
            @blur.stop="editTitle = false"
          />
        </div>
        <button v-show="!showDescription" @click="editTitle = !editTitle">
          {{ editTitleButton }}
        </button>
      </div>
    </div>
    <div v-show="showDescription">
      <textarea
        :disabled="!editDescription"
        v-model="task.itemDesc"
        @blur.stop="editDescription = false"
      ></textarea>
    </div>
    <div>
      <p class="itemStatus">{{ task.itemStatus }}</p>
    </div>
    <div id="buttonsWrapper">
      <button
        v-show="showDescription"
        @click="editDescription = !editDescription"
      >
        {{ editDescriptionButton }}
      </button>
      <button id="statusToggleButton" @click="setStatusButton">
        {{ statusButton }}
      </button>
      <button id="deleteButton" @click="moveToDeleted">
        Delete
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    taskDetails: {
      taskTitle: String,
      taskDescription: String,
      taskStatus: String,
      taskId: Number,
    },
  },
  data() {
    return {
      showDescription: false,
      editDescription: false,
      editTitle: false,
      task: {
        itemTitle: this.taskDetails.taskTitle,
        itemDesc: this.taskDetails.taskDescription,
        itemStatus: this.taskDetails.taskStatus,
        itemId: this.taskDetails.taskId,
      },
    };
  },
  methods: {
    setStatusButton() {
      this.task.itemStatus = this.task.itemStatus === "todo" ? "done" : "todo";
    },
    moveToDeleted() {
      this.task.itemStatus = "deleted";
    },
  },
  updated() {
    this.$emit("task-update", this.task);
  },
  computed: {
    editTitleButton() {
      return this.editTitle ? "save" : "edit";
    },
    editDescriptionButton() {
      return this.editDescription ? "save" : "edit";
    },
    statusButton() {
      return this.task.itemStatus === "todo" ? "Done" : "Todo";
    },
  },
};
</script>

<style scoped>
.clickable {
  cursor: pointer;
}

.posAbsolute {
  position: absolute;
}

#wrapper {
  background-color: #ececec;
  border-radius: 10px;
}

#wrapper button {
  background-color: black;
  border: none;
  color: white;
  border-radius: 5px;

  cursor: pointer;
  padding: 3px 15px;
}

#buttonsWrapper {
  width: 100%;

  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 30px;
  padding-bottom: 20px;
}

.itemStatus {
  position: relative;
  top: 0;
}

textarea {
  border: none;
  font-size: 16px;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  resize: none;
}
</style>
