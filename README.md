# To-Do List Tool

A beautiful, feature-rich to-do list application built with vanilla HTML, CSS, and JavaScript. No frameworks or build tools required - just open `index.html` in your browser!

![To-Do List Preview](https://img.shields.io/badge/Status-Active-brightgreen)

## Features

### Task Management
- **Three-column layout**: "Working on this now", "To do next", and "Done"
- **Drag and drop**: Reorder tasks within columns or move them between columns
- **Task completion**: Click the checkbox to mark tasks as done
- **Comments**: Add comments to any task (supports text and images)
- **Clickable links**: URLs in tasks and comments are automatically converted to clickable links

### Organization
- **Week separators**: Completed tasks are automatically grouped by calendar week
- **Smart sorting**: Most recently completed tasks appear at the top of the Done column
- **Persistent storage**: All tasks are saved to your browser's localStorage

### Customization
- **Editable title**: Click the title to customize it
- **Draggable elements**: Move the title and Elmo mascot anywhere on the screen (desktop only)
- **Resizable container**: Drag the edges of the main container to resize it
- **Custom mascot**: Upload your own image to replace Elmo

### Export Options
- **PDF export**: Print your to-do list to PDF
- **Excel/CSV export**: Download tasks as a spreadsheet

### Mobile Friendly
- Responsive design that works on tablets and phones
- Touch-friendly button sizes
- Single-column layout on smaller screens

---

## How It Was Created

This tool was built using **pure web technologies** with no external dependencies (except Google Fonts):

### Technologies Used

| Technology | Purpose |
|------------|---------|
| **HTML5** | Document structure |
| **CSS3** | Styling, animations, responsive design |
| **JavaScript (ES6+)** | Interactivity, data management |
| **localStorage API** | Persistent data storage |
| **Drag and Drop API** | Task reordering |
| **Google Fonts** | Custom typography (Fredoka, Caveat) |

### Architecture

The entire application is contained in a single `index.html` file for maximum portability:

```
index.html
├── <head>
│   ├── Meta tags & viewport
│   ├── Google Fonts imports
│   └── <style> - All CSS (including responsive breakpoints)
│
├── <body>
│   ├── Title container (draggable)
│   ├── Elmo mascot (draggable, resizable)
│   ├── Main container
│   │   ├── Export buttons
│   │   └── Three columns (drag-drop zones)
│   │       ├── Column 1: Working on this now
│   │       ├── Column 2: To do next
│   │       └── Column 3: Done (with week separators)
│   │
│   └── <script> - All JavaScript
│       ├── Task data management
│       ├── Render functions
│       ├── Event handlers
│       ├── Drag and drop logic
│       ├── localStorage persistence
│       └── Export functions
```

### Data Storage

Tasks are stored in `localStorage` as a JSON array:

```javascript
// Structure of a task
{
    text: "Task description",
    completed: false,
    completedAt: null,  // timestamp when completed
    comments: [
        { text: "Comment text", image: "base64..." }
    ]
}

// Tasks are organized by column index
tasks = [
    [...],  // Column 0: Working on this now
    [...],  // Column 1: To do next
    [...]   // Column 2: Done
]
```

---

## How to Modify the Tool

### Changing Colors

Find the CSS section (inside `<style>` tags) and modify these key properties:

```css
/* Main container background */
.container {
    background: white;  /* Change this */
}

/* Title styling */
h1 {
    background: #a0a0a0;  /* Title background */
    color: #444;          /* Title text color */
    border: 2px solid #666;
}

/* Add button */
.add-btn {
    background: linear-gradient(135deg, #ccb000 0%, #e6d940 100%);
}

/* Completed task color */
.task.completed .task-text {
    color: #888;
}
```

### Changing Fonts

Update the Google Fonts import and CSS:

```html
<!-- In <head>, change the font import -->
<link href="https://fonts.googleapis.com/css2?family=YourFont&display=swap" rel="stylesheet">
```

```css
/* Then update the font-family */
h1 {
    font-family: 'YourFont', sans-serif;
}
```

### Adding a New Column

1. Add HTML for the new column:
```html
<div class="column" data-column="3">
    <h3 class="column-title">New Column</h3>
    <ul class="task-list" id="column-3"></ul>
</div>
```

2. Update the CSS grid:
```css
.columns-container {
    grid-template-columns: repeat(4, 1fr);  /* Change 3 to 4 */
}
```

3. Update JavaScript to include the new column:
```javascript
let tasks = [[], [], [], []];  // Add empty array for column 4
```

### Changing the Mascot Permanently

Replace the base64 image data in the HTML:

1. Convert your image to base64 (use an online converter)
2. Find this line in the HTML:
```html
<img src="data:image/jpeg;base64,..." class="elmo-image">
```
3. Replace the base64 string with your image data

### Modifying Week Separator Labels

Find the `getWeekInfo` and `formatDateRange` functions in the JavaScript:

```javascript
function getWeekInfo(timestamp) {
    // Modify week calculation logic here
}

function formatDateRange(weekStart) {
    // Modify date format here
    // Current format: "Feb 10 - Feb 16"
}
```

### Adding New Features

The codebase follows these patterns:

1. **Add UI elements** in the HTML section
2. **Style them** in the `<style>` section
3. **Add interactivity** in the `<script>` section
4. **Persist data** using `localStorage.setItem()` and `localStorage.getItem()`

Example - Adding a due date to tasks:

```javascript
// 1. Modify the task creation
function addTask(columnIndex, text) {
    const task = {
        text: text,
        completed: false,
        dueDate: null,  // Add new field
        comments: []
    };
    // ...
}

// 2. Update renderTasks to display due date
// 3. Add UI for setting due date
// 4. Save to localStorage (automatic with existing saveTasks())
```

---

## Browser Compatibility

| Browser | Support |
|---------|---------|
| Chrome | ✅ Full support |
| Firefox | ✅ Full support |
| Safari | ✅ Full support |
| Edge | ✅ Full support |
| Mobile browsers | ✅ Responsive design |

---

## Local Storage Keys

The app uses these localStorage keys:

| Key | Description |
|-----|-------------|
| `tasks` | All task data (JSON array) |
| `customTitle` | User's custom title text |
| `containerSize` | Saved container dimensions |
| `elmoPosition` | Elmo mascot position |
| `titlePosition` | Title position |
| `elmoImageData` | Custom mascot image (base64) |
| `elmoImageSize` | Mascot image dimensions |
| `elmoImageVisible` | Whether mascot is shown |

To reset all data, open browser console and run:
```javascript
localStorage.clear();
location.reload();
```

---

## License

This project is open source and available for personal and commercial use.

---

## Credits

- Built with [Cursor](https://cursor.sh/) AI-assisted development
- Fonts from [Google Fonts](https://fonts.google.com/)
- Default mascot: Elmo from Sesame Street
