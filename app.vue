<template>
  <div class="list-task">
    <h2>- TO DO LIST</h2>
    <div v-if="tasks.length === 0" class="empty-state">No tasks</div>
    <div v-else>
      <div
        v-for="(task, index) in tasks"
        :key="index"
        class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
      >
        <input
          type="checkbox"
          name="status"
          :id="'task' + index"
          class="me-2 mt-2"
          :checked="task.isDone"
        />
        <div class="d-flex flex-column">
          <div
            class="title-task mb-1"
            :class="{ success: task.isDone }"
            :style="task.isDone ? 'text-decoration: line-through' : ''"
          >
            {{ task.title }}
          </div>
          <div class="description-task small text-muted">
            {{ task.description }}
          </div>
        </div>
        <button class="delete-button" @click="deleteTask(index)">Delete</button>
      </div>
    </div>
    <div class="action py-2">
      <a
        href="#"
        class="add-button"
        v-if="!isCreating"
        @click="isCreating = !isCreating"
        >Add Task</a
      >
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input
              class="form-control border-0 mb-2"
              placeholder="Title"
              type="text"
              v-model="newTitle"
            />
            <textarea
              class="form-control border-0 small"
              placeholder="Description"
              rows="3"
              v-model="newDescription"
            ></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="addTask">Save</button>
          <button class="btn btn-outline-secondary" @click="cancelTask">
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          title: "Task 1",
          description: "Description 1",
          isDone: true,
        },
      ],
      isCreating: false,
      newTitle: "",
      newDescription: "",
    };
  },
  methods: {
    addTask() {
      if (this.newTitle) {
        console.log(`this is ${this.newTitle}`);
        console.log(`this is ${this.newDescription}`);

        this.tasks.push({
          title: this.newTitle,
          description: this.newDescription,
          isDone: false,
        });
        this.newTitle = "";
        this.newDescription = "";
        this.isCreating = false;
      }
    },
    cancelTask() {
      this.newTitle = "";
      this.newDescription = "";
      this.isCreating = false;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style>
@import "bootstrap/dist/css/bootstrap.css";

.success {
  text-decoration: line-through;
}
</style>
