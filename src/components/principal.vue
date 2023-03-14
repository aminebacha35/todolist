<template>
  <div>
    <h1>Ma liste de tâches</h1>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed">
        <span v-if="!task.editing">{{ task.name }}</span>
        <input v-else v-model="task.name" @keyup.enter="saveTask(index)" @keyup.esc="cancelEdit(index)">
        <button @click="editTask(index)" v-if="!task.editing">Modifier</button>
        <button @click="deleteTask(index)">Supprimer</button>
      </li>
    </ul>
    <div>
      <input type="text" v-model="newTaskName">
      <button @click="addTask">Ajouter</button>
    </div>
    <div>
      <button @click="deleteAllTasks">Supprimer tout</button>
    <button @click="completeAllTasks">Tout terminer</button>
    </div>
  </div>
  <p>Nombre de tâches : {{ countTasks() }}</p>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { name: 'Tâche 1', completed: false, editing: false },
        { name: 'Tâche 2', completed: true, editing: false },
        { name: 'Tâche 3', completed: false, editing: false }
      ],
      newTaskName: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTaskName.trim() === '') {
        return;
      }
      this.tasks.push({ name: this.newTaskName, completed: false, editing: false });
      this.newTaskName = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.tasks[index].editing = true;
    },
    saveTask(index) {
      if (this.tasks[index].name.trim() === '') {
        return;
      }
      this.tasks[index].editing = false;
    },
    cancelEdit(index) {
      this.tasks[index].editing = false;
    },

    deleteAllTasks() {
      this.tasks = [];
    },

    completeAllTasks() {
      this.tasks.forEach((task) => {
        task.completed = true;
      });
    },

    countTasks() {
      return this.tasks.length;
    }
  }
};
</script>
