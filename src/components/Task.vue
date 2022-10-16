<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input
          type="text"
          placeholder="New Task"
          v-model="newTask"
          @keyup.enter="addTask"
        />
        <button @click="addTask" class="add-task">+ Add</button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul v-for="(task, index) in filteredTodos" :key="task.id">
          <task-item
            v-bind:task="task"
            :key="task.id"
            @remove="removeTask(index)"
            @complete="completeTask(task)"
          ></task-item>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="hideCompleted = !hideCompleted">
          {{ hideCompleted ? "Show all" : "Hide completed" }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./Task-item.vue";
export default {
  name: "Task",
  props: ["tasks"],
  components: {
    TaskItem,
  },
  data() {
    return {
      newTask: "",
      hideCompleted: false,
    };
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted ? this.tasks.filter((t) => !t.completed) : this.tasks;
    },
  },
  methods: {
    addTask() {
      if (this.newTask.trim().length > 0) {
        let id = 0;
        if (this.tasks.length > 0) {
          id = this.tasks[this.tasks.length - 1].id + 1;
        }
        let task = {
          id: id,
          title: this.newTask,
          completed: false,
        };
        this.tasks.push(task);
        this.newTask = "";
      }
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style>
#app {
  padding: 60px 0;
}

.container {
  max-width: 480px;
  margin: 0 auto;
  padding: 0 15px;
}

input[type="text"] {
  width: 100%;
  height: 50px;
  font: 15px/1.4 "Poppins", sans-serif;
  padding: 15px;
  background: #f3f3f3;
  color: #333;
  border: 1px solid transparent;
  border-radius: 10px;
  transition: border 0.3s linear;
}

input[type="text"]:focus {
  outline: none;
  border: 1px solid #4ec5c1;
}

button {
  cursor: pointer;
  font: 15px/1.4 "Poppins", sans-serif;
  color: #555;
  transition: all 0.3s linear;
}

button:focus {
  outline: none;
}

h1 {
  font-size: 22px;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
/* 
task 
----
*/
.task {
  background: #fff;
  border-radius: 25px;
  padding: 30px;
  box-shadow: 0px 0px 40px 0px rgba(0, 0, 0, 0.1);
}

.title {
  text-align: center;
  margin: 0 0 20px;
}

.form {
  position: relative;
  margin: 0 0 30px;
}
.form button {
  background-color: #4ec5c1;
  padding: 14px 12px;
  font-weight: 900;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  transition: 0.2s background ease-in;
  font-size: 1rem;
  border: none;
  color: #fff;
  position: absolute;
  top: 50%;
  right: 0px;
  transform: translateY(-50%);
}
.form button:hover {
  background-color: #3cb6b2;
  transition: all 0.2s linear;
}

.clearBtns {
  display: flex;
  justify-content: space-between;
  margin: 0 0 20px;
}

.clearBtns button {
  width: 100%;
  font-weight: 700;
  background: #4ec5c1;
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px;
  margin: 0 5px;
}

.clearBtns button:hover {
  background: #333;
}
/* 
task items
----------
*/
.pendingTasks {
  padding: 0 6px;
}

.taskItems {
  padding: 0 10px;
}

.taskItems li {
  display: flex;
  justify-content: space-between;
  margin: 0 0 20px;
}

.taskItems button {
  background: none;
  border: none;
}

.taskItems button:hover {
  color: #4ec5c1;
}

.fa-trash-alt:hover {
  color: #ff0000;
}

.taskItems .toggle i {
  margin: 0 10px 0 0;
  font-size: 14px;
}

.taskItems .toggle.toggle-completed {
  text-decoration: line-through;
}
</style>
