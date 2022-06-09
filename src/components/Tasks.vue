<template>
    <div class="container">
    <Header :title = "tasks.title" @toggle-add-task="toggleAddTask" :showAddTask="showAddTask" />
     <div v-show="showAddTask" >
      <AddTask @add-task="addTask"/>
    </div>
      <Task v-for="task in tasks.tasks"
        :key="task.id"
        :task="task"
        @toggle-reminder="$emit('toggle-reminder', { listIndex: this.tasks.listId, taskIndex: task.id })"
        @delete-task="$emit('delete-task', { listIndex: this.tasks.listId, taskIndex: task.id })"
      />
    <Button @btn-click="$emit('delete-tasks-list', tasks.listId)" :text = "'Delete'" :color = "'red'"/>
    <Button @btn-click="$emit('toggle-edit', tasks)" :text = "'Edit'" :color = "'blue'"/>
  </div>
</template>

<script>
import Task from "./Task";
import Header from "./Header";
import AddTask from './AddTask'
import Button from "./Button";

export default {
  name: 'Tasks',
  components: {
    Task,
    Header,
    AddTask,
    Button
  },
  props: {
    tasks: Object,
  },
  data () {
    return {
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask () {
      this.showAddTask = !this.showAddTask
    },
    addTask (newTasks) {
      this.$emit('add-task', {listIndex: this.tasks.listId, newTasks })
    }
  },
  emits: ['delete-task', 'toggle-reminder']
};
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
</style>