# Fully-functional-To-Do-List-application-using-ES6-JavaScript-
## Aim:
### To Create a fully functional To-Do-List application using ES6 JavaScript.

### Program:
### Index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Work To-Dos</h1>
        <p>Enter text into the input field to add items to your list.</p>
        <p>Click the item to mark it as complete.</p>
        <p>Click the "X" to remove the item from your list.</p>
        <form id="task-form">
            <input type="text" id="task-title" placeholder="New item...">
            <input type="text" id="task-desc" placeholder="Description...">
            <input type="date" id="task-date">
            <button type="submit">Add Task</button>
        </form>
        <ul id="task-list"></ul>
    </div>
    <script type="module" src="js.js"></script>
</body>
</html>
```
### Styles.css
```
body {
    font-family: Arial, sans-serif;
    background-color: #58a259;
    color: #ffffff;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    background: #ffffff;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    color: #333333;
    max-width: 500px;
    width: 100%;
}

form {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

form input, form button {
    padding: 10px;
    margin: 5px 0;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    background: #f9f9f9;
    margin: 5px 0;
    padding: 10px;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

li.completed {
    text-decoration: line-through;
    color: #999999;
}

li button {
    background: #ff4444;
    border: none;
    color: #ffffff;
    padding: 5px 10px;
    border-radius: 4px;
    cursor: pointer;
}

li button:hover {
    background: #ff2222;
}
```
### js.js
```
export default class Task {
    constructor(title, description, dueDate, completed = false) {
        this.title = title;
        this.description = description;
        this.dueDate = dueDate;
        this.completed = completed;
    }
}
```
### ToDoList.js
```
import Task from './Task.js';

export default class ToDoList {
    constructor() {
        this.tasks = JSON.parse(localStorage.getItem('tasks')) || [];
    }

    addTask(task) {
        this.tasks.push(task);
        this.saveTasks();
    }

    editTask(index, updatedTask) {
        this.tasks[index] = updatedTask;
        this.saveTasks();
    }

    deleteTask(index) {
        this.tasks.splice(index, 1);
        this.saveTasks();
    }

    toggleTaskCompletion(index) {
        this.tasks[index].completed = !this.tasks[index].completed;
        this.saveTasks();
    }

    filterTasks(filter) {
        return this.tasks.filter(task => {
            if (filter === 'all') return true;
            if (filter === 'completed') return task.completed;
            if (filter === 'incomplete') return !task.completed;
        });
    }

    saveTasks() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }

    fetchTasksFromAPI(apiEndpoint) {
        fetch(apiEndpoint)
            .then(response => response.json())
            .then(data => {
                this.tasks = data.map(task => new Task(task.title, task.description, task.dueDate, task.completed));
                this.saveTasks();
            });
    }
}
```
### Main.js
```
import Task from 'js.js';
import ToDoList from 'ToDoList.js';

const todoList = new ToDoList();
const taskListElement = document.getElementById('task-list');
const taskForm = document.getElementById('task-form');
const taskTitle = document.getElementById('task-title');
const taskDesc = document.getElementById('task-desc');
const taskDate = document.getElementById('task-date');

function renderTasks() {
    taskListElement.innerHTML = '';
    todoList.tasks.forEach((task, index) => {
        const taskElement = document.createElement('li');
        taskElement.className = task.completed ? 'completed' : '';
        taskElement.innerHTML = `
            <span>${task.title} - ${task.description} - ${task.dueDate}</span>
            <button onclick="deleteTask(${index})">X</button>
            <input type="checkbox" ${task.completed ? 'checked' : ''} onclick="toggleTaskCompletion(${index})">
        `;
        taskListElement.appendChild(taskElement);
    });
}

taskForm.addEventListener('submit', event => {
    event.preventDefault();
    const newTask = new Task(taskTitle.value, taskDesc.value, taskDate.value);
    todoList.addTask(newTask);
    renderTasks();
    taskTitle.value = '';
    taskDesc.value = '';
    taskDate.value = '';
});

window.deleteTask = index => {
    todoList.deleteTask(index);
    renderTasks();
};

window.toggleTaskCompletion = index => {
    todoList.toggleTaskCompletion(index);
    renderTasks();
};

document.addEventListener('DOMContentLoaded', () => {
    renderTasks();
});
```
### Output:
![D4 1](https://github.com/user-attachments/assets/e35d7f57-2728-4846-811d-9f2dec64538e)

![D4 2](https://github.com/user-attachments/assets/400b94bb-e4f3-446e-b324-2080b63b730d)

![D4 3](https://github.com/user-attachments/assets/a7101a77-ea4d-4c0e-aa24-68b1f14bf78f)

### Result:
Thus,fully functional To-Do-List application using ES6 JavaScript was executed successfuly.


