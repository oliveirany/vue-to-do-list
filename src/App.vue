<template>
  <main>
    <div  id="todo">
      <input v-model="newTaskText" type="text" placeholder="Type a new task...">
      <button @click="addNewTask" :disabled="newTaskText ? false : true">+</button>
      <ul>
        <li v-for="task in tasks" :key="task.id" class="tasks">
          <input type="checkbox" name="taskCheck" id="taskCB">
          <label :contenteditable="task.editable">{{ task.text }}</label>
          <button @click="updateTask(task.id)">{{ !task.editable ? 'Update' : 'Confirm' }}</button>
          <button @click="removeTask(task.id)">Delete</button>
        </li>
      </ul>
    </div>
  </main>
</template>

<script lang="ts">
export default {
  data() {
    return {
      tasks: [] as { id: number; text: string; editable: boolean }[],
      newTaskText: ''
    }
  },
  methods: {
    addNewTask() {
      this.tasks.push({ id: new Date().getTime(), text: this.newTaskText, editable: false })
      this.newTaskText = ''
    },
    removeTask(taskId: number) {
      this.tasks = this.tasks.filter(t => t.id !== taskId)
    },
    updateTask(taskId: number) {
      this.tasks.map((task) => {
        task.editable = task.id === taskId ? !task.editable : task.editable
      })
    }
  }
}
</script>

<style>
  #todo {
    margin-top: 250px;
    margin-left: 550px;
  }
  .tasks {
    list-style-type: none;
  }
</style>