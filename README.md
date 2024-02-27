
# Habit Maker Web App 🚀

## Overview

Welcome to Habit Maker, a simple web application built with React that helps you manage your daily tasks and habits. This README will guide you through the structure of the project and provide insights into how the key components work.

## How to Use

### 1. Installation

Make sure you have [Node.js](https://nodejs.org/) installed.

```bash
# Clone the repository
git clone https://github.com/Arihant-Singh-Rana/Habit_Maker.git

# Navigate to the project directory
cd habit-maker

# Install dependencies
npm install
```

### 2. Running the App

```bash
# Run the app locally
npm start
```

Visit `http://localhost:3000` in your browser to use the Habit Maker app.

## Project Structure

### `App.js`

The main component that renders the entire application. It includes the `HabitInput` for adding new habits and `ShowHabits` to display the existing ones.

```jsx
import React, { useState } from "react";
import HabitInput from "./Components/HabitInput";
import TaskContainer from "./Components/TaskContainer";
import ShowHabits from "./Components/ShowHabits";

function App() {
  // State to manage habits
  const [showHabits, setShowHabits] = useState([]);

  // Function to add a new habit
  function addHabitData(habitData) {
    setShowHabits([...showHabits, habitData]);
  }

  // Function to delete a habit
  function deleteHabit(index) {
    const temp = [...showHabits];
    temp.splice(index, 1);
    setShowHabits([...temp]);
  }

  // JSX structure
  return (
    <div>
      <h1 className="title">Habit Maker</h1>
      <TaskContainer>
        <HabitInput addHabitData={addHabitData} />
        <ShowHabits show={showHabits} deleteit={deleteHabit} />
      </TaskContainer>
    </div>
  );
}

export default App;
```

### `HabitInput.js`

A component responsible for taking user input to add a new habit. It includes form fields for 'What,' 'Where,' 'Why,' and 'Date.'

```jsx
import React, { useState } from "react";
import style from "./HabitInput.module.css";

function HabitInput({ addHabitData }) {
  // State to manage habit input
  const [habitData, setHabitData] = useState({ what: "", where: "", why: "", date: "" });

  // Function to handle input changes
  function handleChange(e) {
    const { id, value } = e.target;
    setHabitData({ ...habitData, [id]: value });
  }

  // Function to handle form submission
  function handleSubmit(e) {
    e.preventDefault();
    // Validation
    if (Object.values(habitData).some((x) => x === "")) {
      alert("Please fill all the fields below before saving");
      return;
    }
    addHabitData(habitData);
    setHabitData({ what: "", where: "", why: "", date: "" });
  }

  // JSX structure
  return (
    <div>
      <form onSubmit={handleSubmit}>
        {/* ... input fields */}
        <button className={style.savebtn}>Save</button>
      </form>
    </div>
  );
}

export default HabitInput;
```

### `ShowHabits.js`

This component displays the list of habits. It includes a delete button for each habit.

```jsx
import React from "react";
import style from "./ShowHabits.module.css";

function ShowHabits({ show, deleteit }) {
  let showTask;

  // If habits exist, map and display them
  if (show.length !== 0) {
    showTask = show.map((task, index) => (
      <tr className={style.row} key={index}>
        {/* ... habit details */}
        <td className={style.data}>
          <button onClick={() => deleteit(index)} className={style.btn}>
            Delete
          </button>
        </td>
      </tr>
    ));
  } else {
    // If no habits, display a message
    showTask = (
      <tr className={style.row}>
        <h1 className={style.nodata}>You Have No Tasks</h1>
      </tr>
    );
  }

  // JSX structure
  return (
    <div>
      <table>{showTask}</table>
    </div>
  );
}

export default ShowHabits;
```

### `TaskContainer.js`

A simple wrapper component for styling purposes.

```jsx
import React from "react";
import Component from "./TaskContainer.module.css";

function TaskContainer({ children }) {
  return <div className={Component.Parent}>{children}</div>;
}

export default TaskContainer;
```

## Contribution

Feel free to contribute by submitting issues or creating pull requests. Let's make Habit Maker even better together!

