<template>
  <div>
    <div class="main_add_task" @click="$emit('add-task-list')">
      <p>Add new list of tasks</p>
    </div>
    <div class="upd">Upd. Double click on the task to change reminder</div>
  </div>
</template>

<script>
  export default {
    name:'AddTaskList',
  };
</script>

<style scoped>
.main_add_task {
  cursor: pointer;
  max-width: 192px;
  max-height: 192px;
  background-color: steelblue;
  color: beige;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  border: 3px solid steelblue;
  border-radius: 10px;
  margin: 70px 10px 0px 50px;
}
p {
  font-size: 30px;
}
.upd {
  margin: 15px 0 0 30px;
  color: green;
  display: flex;
  max-width: 235px;
  flex-wrap: wrap;
  text-align: center;
}

</style>