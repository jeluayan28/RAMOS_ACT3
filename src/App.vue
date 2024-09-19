<template>
  <div class="app-container">
    <!-- Navbar -->
    <nav class="navbar">
      <div class="navbar-title">Start Your Day</div>
    </nav>

    <div class="task-list-container">
      <!-- Task input form -->
      <div class="navbar-title">To-Do List</div>
      <div class="task-input">
        <input
          type="text"
          v-model="newTask"
          placeholder="Add a new task"
          @keyup.enter="addTask"
        />
        <button @click="addTask">{{ editingIndex !== null ? 'Update Task' : 'Add Task' }}</button>
      </div>

      <!-- Task table -->
      <table class="task-table">
        <thead>
          <tr>
            <th>#</th>
            <th>Task</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ task }}</td>
            <td class="actions">
              <span @click="editTask(index)" class="edit-text">Edit</span>
              <span @click="deleteTask(index)" class="delete-text">Delete</span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: ['Practice Public Speaking', 'Study Your Lessons', 'Read a book','Work out','Have a Haircut'],
      editingIndex: null, // Keep track of the index being edited
    };
  },
  methods: {
    // Add or update a task
    addTask() {
      if (this.newTask.trim()) {
        if (this.editingIndex !== null) {
          this.tasks.splice(this.editingIndex, 1, this.newTask); // Update task
          this.editingIndex = null; // Reset editing mode
        } else {
          this.tasks.push(this.newTask); // Add new task
        }
        this.newTask = ''; // Clear input field
      }
    },
    // Edit a task
    editTask(index) {
      this.newTask = this.tasks[index];
      this.editingIndex = index;
    },
    // Delete a task
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style scoped>
/* Navbar styling */
.navbar {
  width: 100%;
  background-color: #2c3e50;
  padding: 15px 0;
  text-align: center;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

.navbar-title {
  color: white;
  font-size: 1.5rem;
  font-weight: bold;
}

.app-container {
  padding-top: 70px; /* Adjust to make space for the fixed navbar */
}

/* Task list container */
.task-list-container {
  width: 100%;
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  background-color: #2c3e5041;
  border-radius: 8px;
}

.task-input {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 20px;
}

.task-input input {
  flex-grow: 1;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #2c3e50;
  margin-right: 10px;
}

.task-input button {
  padding: 8px 12px;
  background-color: #2c3e50ac;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.task-input button:hover {
  background-color: #2aa188;
}

.task-table {
  width: 100%;
  background-color: #fff;
  border-collapse: collapse;
  border-radius: 8px;
}

.task-table th,
.task-table td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.actions {
  display: flex;
  justify-content: space-around;
}

/* Styling for Edit and Delete actions */
.edit-text {
  cursor: pointer;
  color: #e67e22; /* Orange for edit */
  margin-right: 10px;
}

.delete-text {
  cursor: pointer;
  color: #e74c3c; /* Red for delete */
}

.edit-text:hover {
  color: #d35400; /* Darker orange on hover */
}

.delete-text:hover {
  color: #c0392b; /* Darker red on hover */
}

/* Responsive styling */
@media (max-width: 600px) {
  .task-list-container {
    width: 95%;
    padding: 15px;
  }

  .task-input {
    flex-direction: column;
  }

  .task-input input {
    margin-right: 0;
    margin-bottom: 10px;
    width: 100%;
  }

  .task-input button {
    width: 100%;
    padding: 10px;
  }

  .task-table th, 
  .task-table td {
    font-size: 0.9rem;
    padding: 8px;
  }

  .actions {
    flex-direction: column;
    align-items: flex-start;
  }

  .edit-text, 
  .delete-text {
    margin-right: 0;
    margin-bottom: 5px;
  }
}
</style>
