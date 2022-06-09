<template>
  <div class="main">
    <div class="form">
        <input class="form_title" type="text" :value="list.title"
          @input="$emit('edit-task-list',{ ...list, title: $event.target.value }, list.listId)"/>
        <div class="form_text">
          <input v-for="task in list.tasks" :key="task.id" type="text" :value="task.text"
            @input="(event) => editTask(event, task.id)"/>
          <Button @btn-click="$emit('toggle-edit', {})" :text = "'Close'" :color = "'black'"/>
        </div>
    </div>
  </div>
</template>

<script>
import Button from './Button';

export default {
  name: 'EditTaskList',
  props: {
    list: Array,
  },
  components: {
    Button
  },
  methods: {
    editTask(event, id) {
      this.list.tasks.forEach((task) => {
        if (task.id === id) {
          task.text = event.target.value;
        }
      });
      this.$emit("edit-task-list", { ...this.list }, this.list.listId);
    },
  },
};
</script>

<style scoped>
.form {
  background-color: steelblue;
  left: 35%;
  top: 10%;
  position: fixed;
  border-radius: 10px;
  border: 2px solid red;
}
input {
  border-radius: 10px;
  background-color: white;
  padding: 10px;
}
.form_title {
  margin: 20px;
  font-size: 30px;
}
.form_text {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}
.form_text input {
  font-size: 24px;
  margin-bottom: 10px;
}

</style>
