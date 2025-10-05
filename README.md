<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mini E-Learning Platform</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f9f9f9;
    }

    header {
      background: #4CAF50;
      color: white;
      padding: 1rem;
      text-align: center;
    }

    .container {
      padding: 2rem;
      max-width: 800px;
      margin: auto;
    }

    .course-list, .lesson-list {
      list-style: none;
      padding: 0;
    }

    .course-item, .lesson-item {
      background: white;
      margin-bottom: 1rem;
      padding: 1rem;
      border-radius: 8px;
      cursor: pointer;
      transition: box-shadow 0.3s ease;
    }

    .course-item:hover, .lesson-item:hover {
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .button {
      background-color: #4CAF50;
      color: white;
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 1rem;
      transition: background-color 0.3s ease;
    }

    .button:hover {
      background-color: #45a049;
    }

    .back-button {
      background-color: #777;
    }

    .completed {
      color: green;
      font-weight: bold;
    }
  </style>
</head>
<body>

<header>
  <h1>Mini E-Learning Platform</h1>
</header>

<div class="container" id="app">
  <!-- Content will be injected here -->
</div>

<script>
  // Sample course data
  const courses = [
    {
      id: 1,
      title: "HTML Basics",
      completed: false,
      lessons: ["Introduction", "Tags & Elements", "Links", "Images"]
    },
    {
      id: 2,
      title: "CSS Fundamentals",
      completed: false,
      lessons: ["Selectors", "Box Model", "Flexbox", "Grid"]
    },
    {
      id: 3,
      title: "JavaScript Essentials",
      completed: false,
      lessons: ["Variables", "Functions", "DOM Manipulation", "Events"]
    }
  ];

  const app = document.getElementById('app');

  function renderHomePage() {
    app.innerHTML = `<h2>All Courses</h2><ul class="course-list">
      ${courses.map(course => `
        <li class="course-item" onclick="viewCourse(${course.id})">
          <strong>${course.title}</strong><br>
          <span class="${course.completed ? 'completed' : ''}">
            ${course.completed ? 'Completed ✔️' : 'In Progress'}
          </span>
        </li>`).join('')}
    </ul>`;
  }

  function viewCourse(id) {
    const course = courses.find(c => c.id === id);
    app.innerHTML = `
      <button class="button back-button" onclick="renderHomePage()">← Back</button>
      <h2>${course.title}</h2>
      <ul class="lesson-list">
        ${course.lessons.map(lesson => `<li class="lesson-item">${lesson}</li>`).join('')}
      </ul>
      <button class="button" onclick="toggleComplete(${id})">
        ${course.completed ? 'Mark as Incomplete' : 'Mark as Completed'}
      </button>
    `;
  }

  function toggleComplete(id) {
    const course = courses.find(c => c.id === id);
    course.completed = !course.completed;
    viewCourse(id);
  }

  // Initial render
  renderHomePage();
</script>

</body>
</html>
