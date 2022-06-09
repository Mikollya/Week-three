<template>
  <div>
    <EditTaskList
      v-if="Object.keys(showEditModal).length > 0"
      :list="showEditModal"
      @edit-task-list="editTaskList"
      @toggle-edit="toggleEdit"
    />
    <div class="main__lists">
      <AddTaskList @add-task-list="addTaskList" />
      <Tasks
        v-for="tasks in list"
        :key="tasks.id"
        :tasks="tasks"
        @add-task="addTask"
        @delete-tasks-list="deleteTaskList"
        @delete-task="deleteTask"
        @toggle-edit="toggleEdit"
        @toggle-reminder="toggleReminder"
      />
    </div>
  </div>
</template>

<script>
import AddTaskList from "./components/AddTaskList";
import EditTaskList from "./components/EditTaskList";
import Tasks from "./components/Tasks";

export default {
  name: "App",
  components: { 
    Tasks, 
    AddTaskList,
    EditTaskList,
    },
  data() {
    return {
      list: [],
      showEditModal: Boolean,
    };
  },
  methods: {
    toggleReminder(value) {
       const index = this.list.findIndex((tasks) => {
          return tasks.listId == value.listIndex;
        });
        console.log (value)

      this.list[index].tasks = this.list[index].tasks.map((task) =>
        task.id === value.taskIndex ? {...task, reminder: !task.reminder} : task)
    },
    deleteTask(value) {
      const index = this.list.findIndex((tasks) => {
        return tasks.listId == value.listIndex;
      });

      if (confirm ("Are u sure?")) {
        this.list[index].tasks = this.list[index].tasks.filter((task) => task.id !== value.taskIndex)
      }
    },
    addTask(value) {
      const index = this.list.findIndex((tasks) => {
        return tasks.listId == value.listIndex;
      });
      this.list[index].tasks = [...this.list[index].tasks, value.newTasks.newTask]
    },
    addTaskList() {
      const newTaskList = 
        {
          listId: Math.floor(Math.random() * 10000),
          title: "Tasks",
          tasks: [{ id: 1, text: "Task", reminder: false }],
        }
      this.list = [...this.list, newTaskList]
    },
    deleteTaskList(id) {
      if (confirm ("Are u sure?")) {
        this.list = this.list.filter((tasks) => tasks.listId !== id  );
      }
    },
    toggleEdit(value) {
      this.showEditModal = value;
    },
    editTaskList(value, id) {
      const index = this.list.findIndex((task) => {
        return task.listId == id;
      });
      this.list[index] = Object.assign(this.list[index], { ...value });
    },
  },
  created () {
    this.list = [
        {
          listId: 1,
          title: "Apointments",
          tasks: [
            { id: 1, text: "Doctors appointment", reminder: false },
            { id: 2, text: "Meeting at School", reminder: true },
            { id: 3, text: "Buying shoes", reminder: false },
          ],
        },
        {
          listId: 2,
          title: "Take charge",
          tasks: [
            { id: 1, text: "Food Shopping", reminder: true },
            { id: 2, text: "Utensils", reminder: false },
            { id: 3, text: "Guitar Playeing", reminder: false },
          ],
        },
      ]
  },
};
</script>

<style rel="stylesheet/scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
}
body {
  font-family: 'Poppins', sans-serif;
}
.main__lists {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}

</style>