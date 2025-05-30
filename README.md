# React To-Do List 📝

A feature-rich, responsive to-do list application built with React that helps you manage your daily tasks efficiently. Features a beautiful background image, persistent local storage, and intuitive task management with real-time editing capabilities.

## ✨ Features

- **Add Tasks**: Easily add new tasks with a clean input interface
- **Inline Editing**: Click the edit icon to modify tasks with a dedicated edit mode
- **Delete Tasks**: Remove individual tasks or clear all tasks at once
- **Task Completion**: Check off completed tasks with visual strike-through effect
- **Persistent Storage**: Tasks are automatically saved to localStorage and persist across browser sessions
- **Dynamic UI States**: Interface adapts based on edit mode vs. view mode
- **Responsive Design**: Works seamlessly on desktop and mobile devices
- **Beautiful UI**: Custom background image with clean, modern styling

## 📸 Screenshots

### Main Interface
![Main Interface](assets/Initial_template.png)
*Clean interface with background image and task list*

### Adding New Tasks
![Adding Tasks](assets/Added_To_Do.png)
*Simple task addition with plus icon button*

### Edit Mode
![Edit Mode](assets/Edit-Mode.png)
![Successfully](assets/Successfully_Edited.png)
*Dedicated edit interface with UPDATE button*

### Completed Tasks
![Completed Tasks](assets/Completed_To_Do.png)
*Visual strike-through for completed items*

## Deleted Tasks
![Deleted Tasks](assets/Deleted_To_Do.png)
*Deleted Single, or Delete all*

## 🛠️ Technologies Used

- **React** (Functional Components)
- **React Hooks** (useState, useEffect)
- **React Icons Kit** - Feather icons for UI elements
- **Local Storage API** - Data persistence
- **CSS3** - Custom styling with background images
- **HTML5** - Semantic structure

## 🏗️ Project Structure

```
To-o-list/
├── public/
│   ├── index.html
├── src/
│   ├── Components/
│   │   └── Form.js          # Main todo component
│   ├── assets/
│   │   └── backgroundImage.jpg
│   ├── App.js               # Main app component
│   ├── index.js             # React DOM render
│   └── index.css            # Global styles
├── package.json
└── README.md
```

## 💻 Key Implementation Details

### 🎣 React Hooks Implementation

**State Management:**
```javascript
const [todoValue, setTodoValue] = useState('');     // Input field value
const [todos, setTodos] = useState(getTodosFromLS()); // Todo items array
const [editForm, setEditForm] = useState(false);    // Edit mode toggle
const [id, setId] = useState();                     // Current editing ID
```

**Local Storage Integration:**
```javascript
// Load todos from localStorage on component mount
const getTodosFromLS = () => {
    const data = localStorage.getItem('Todos');
    return data ? JSON.parse(data) : [];
}

// Save todos to localStorage whenever todos state changes
useEffect(() => {
    localStorage.setItem('Todos', JSON.stringify(todos));
}, [todos])
```

### 🔧 Core Functionality

**Adding Tasks:**
- Each task gets a unique timestamp-based ID
- Form validation ensures non-empty tasks
- Auto-clears input after submission

**Editing Tasks:**
- Switches to dedicated edit mode interface
- Pre-populates input with existing task text
- Hides checkboxes and action buttons during editing

**Task Completion:**
- Toggle checkbox updates completion state
- Visual feedback with strike-through text
- Completion state persists in localStorage

**Smart UI States:**
- Edit mode hides unnecessary UI elements
- Conditional rendering based on `editForm` state
- Different button styles for add vs. update actions

## 🎨 Styling Features

- **Custom Background**: Full-screen background image with proper scaling
- **Responsive Layout**: 500px max-width container with auto-centering
- **Interactive Elements**: Hover effects and cursor changes
- **Visual Feedback**: Strike-through for completed tasks

## 🔍 Code Highlights

### Unique ID Generation
```javascript
const date = new Date();
const time = date.getTime();
let todoObject = {
    ID: time,
    TodoValue: todoValue,
    completed: false
}
```

### Dynamic Checkbox Handling
```javascript
const handleCheckbox = (id) => {
    let todoArray = [];
    todos.forEach((todo) => {
        if(todo.ID === id) {
            todo.completed = !todo.completed;
        }
        todoArray.push(todo);
    });
    setTodos(todoArray);
}
```

### Conditional Rendering Pattern
```javascript
{editForm === false && (
    <input type='checkbox' 
           checked={individualTodo.completed}
           onChange={() => handleCheckbox(individualTodo.ID)}/>
)}
```

## 🚀 Usage Guide

### Adding a Task
1. Type your task in the input field
2. Click the **+** button or press Enter
3. Task appears in the list with checkbox and action icons

### Editing a Task
1. Click the **edit icon** (✏️) next to any task
2. Interface switches to edit mode with pre-filled input
3. Modify the text and click **UPDATE**
4. Returns to normal view with updated task

### Managing Tasks
- **Complete**: Check the checkbox to mark as done (adds strike-through)
- **Delete Single**: Click the trash icon to remove a specific task
- **Delete All**: Use "Delete All Items" button to clear everything
