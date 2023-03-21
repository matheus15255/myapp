<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h1>Minha lista de tarefas</h1>
        <form class="form-inline" @submit.prevent="addTask">
          <div class="form-group">
            <input type="text" class="form-control" v-model="newTask" placeholder="Adicionar nova tarefa">
            <button type="submit" class="btn btn-primary">Adicionar</button>
          </div>
        </form>
      </div>
      <div class="card-body">
        <div class="form-group">
          <label for="filter">Filtrar por:</label>
          <select id="filter" class="form-control" v-model="filter">
            <option value="all">Todas</option>
            <option value="active">Ativas</option>
            <option value="completed">Concluídas</option>
          </select>
        </div>
        <ul class="list-group">
          <li v-for="(task, index) in filteredTasks" :key="index" class="list-group-item">
    <input type="checkbox" :checked="task.completed" @change="updateTask(task)">
    <span :class="{ 'completed': task.completed }">{{ task.name }}</span>
    <button class="btn btn-danger btn-sm float-right" @click="removeTask(task)">Remover</button>
</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { name: 'Comprar pão', completed: false },
        { name: 'Fazer exercício', completed: true },
        { name: 'Ler livro', completed: false }
      ],
      newTask: '',
      filter: 'all'
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === "completed") {
        return this.tasks.filter(task => task.completed);
      } else if (this.filter === "active") {
        return this.tasks.filter(task => !task.completed);
      } else {
        return this.tasks;
      }
    }
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({ name: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    updateTask(task) {
      task.completed = !task.completed;
    },
    removeTask(task) {
      this.tasks.splice(this.tasks.indexOf(task), 1);
    }
  }
};
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.card {
  width: 80%;
  max-width: 600px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f8f9fa;
  border-bottom: 1px solid #ccc;
}

.card-header h1 {
  margin: 0;
}

.card-body {
  padding: 10px;
}

.form-inline {
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-inline .form-group {
  display: flex;
  margin: 0;
}

.form-inline .form-control {
  flex: 1;
  margin-right: 0;
}

.list-group-item {
display: flex;
justify-content: space-between;
align-items: center;
}

.completed {
text-decoration: line-through;
}
</style>
<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.card {
  width: 80%;
  max-width: 600px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f8f9fa;
  border-bottom: 1px solid #ccc;
}

.card-header h1 {
  margin: 0;
}

.card-body {
  padding: 10px;
}

.form-inline {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.form-inline .form-group {
  display: flex;
  margin: 0;
}

.form-inline .form-control {
  flex: 1;
  margin-right: 0;
  border-radius: 5px;
}

.form-inline .btn {
  border-radius: 5px;
}

.list-group-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: none;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #f8f9fa;
  border-radius: 5px;
}

.list-group-item:last-child {
  margin-bottom: 0;
}

.list-group-item:hover {
  background-color: #e9ecef;
}

.list-group-item .form-check-input {
  margin-right: 10px;
}

.completed {
  text-decoration: line-through;
}
</style>