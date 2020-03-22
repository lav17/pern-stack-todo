# PERN Full Stack Todo

* PostgreSQL Express React Node (PERN) full-stack app, integrates React frontend with Node.js backend. Tutorial code (see 'Inspiration' below)

*** Note: to open web links in a new window use: _ctrl+click on link_**

## Table of contents

* [General info](#general-info)
* [Screenshots](#screenshots)
* [Technologies](#technologies)
* [Setup](#setup)
* [Features](#features)
* [Status](#status)
* [Inspiration](#inspiration)
* [Contact](#contact)

## General info

### Backend

* PostgreSQL needs to be installed and running - I started it from my Windows 10 PostgreSQL 12 dropdown option 'SQL shell (psql)'
* Postman used to test the backend before frontend was available

### Frontend

* React frontend includes a simple todo list with a user input field and a table of todos below. User can edit and delete todos.
* [JavaScript XML (JSX)](https://reactjs.org/docs/introducing-jsx.html) used to write HTML elements in Javascript
* [React Fragments](https://reactjs.org/docs/fragments.html) used to show table of todos as a row with columns in the DDM

## Screenshots

![Backend screenshot](./img/postgresql.png)
![Frontend & backend screenshot](./img/todos.png)
![Frontend screenshot](./img/edit.png)

## Technologies - Backend

* [PostgreSQL v12.2](https://www.postgresql.org/)
* [PostgreSQL Installer for Windows](https://www.postgresqltutorial.com/install-postgresql/)
* [Express.js middleware v4.17.1](https://expressjs.com/)
* [Node.js v12.4.0](https://nodejs.org/es/)
* [Nodemon](https://www.npmjs.com/package/nodemon) npm module so backend server will automatically restart after code changes
* [Postman API](https://www.postman.com/downloads/) to simulate a frontend

## Technologies - Frontend

* [React framework v16.13.1](https://reactjs.org/)
* [Bootstrap v4.4.1](https://getbootstrap.com/) component library

## Setup - Backend

* Change to `/server` directory
* Install dependencies using `npm i`
* Install [nodemon v2.0.2](https://www.npmjs.com/package/nodemon) globally if you don't already have it
* Install [PostgreSQL](https://www.postgresql.org/) & run it (requires the password you created during installation)
* Add database access credentials to `db.js` - recommend installing [npm dotenv](https://www.npmjs.com/package/dotenv) & using .env to hide credentials if commiting to Github
* Run `nodemon server` for a dev server
* `http://localhost:5000/` can be accessed for CRUD operations such as POST, GET, PUT, DELETE etc. using Postman

## Setup - Frontend

* Change to `/client` directory
* Install dependencies using `npm i`. (I have not tried this method and cannot be sure it will work)
* Alternatively - and better - create new React project using `npx create-react-app my-app`
* run `npm start`. Frontend will open at `http://localhost:3000/`

## Code Examples - Backend

* backend `index.js`: express post method used to add new todo [description] to postgreSQL database using SQL INSERT INTO statement

```javascript
// create a todo
app.post('/todos', async (req, res) => {
  try {
    const { description } = req.body;
    const newTodo = await pool.query(
      "INSERT INTO todo (description) VALUES($1) RETURNING *",
      [description]
    );

    res.json(newTodo.rows[0]);
  } catch (err) {
    console.error(err.message);
  }
})
```

## Code Examples - Frontend

* function that runs when user presses 'Add' button: the input body (description) is converted from a JavaScript object to a JSON string & POSTed to the todo database

```javascript
  const onSubmitForm = async e => {
    e.preventDefault();
    try {
      const body = { description };
      const response = await fetch("http://localhost:5000/todos", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(body)
      });

      console.log("Successfully added todo: ", response);
      window.location = "/";
    } catch (err) {
      console.error(err.message);
    }
  };
```

## Features - Backend

* All data stored in PostgreSQL database that can also be viewed and changed from the PostgreSQL shell (psql)

## Features - Frontend

* React app created from the command prompt using [Create React App](https://reactjs.org/docs/create-a-new-react-app.html)
* Uses the [Bootstrap basic table](https://www.w3schools.com/bootstrap/bootstrap_tables.asp) to list todos
* [Bootstrap 4 Modal](https://www.w3schools.com/bootstrap4/bootstrap_modal.asp) dialog box

## Status & To-Do List

* Status: Working front and back ends.
* To-Do: Add commenting. Add functionality.

## Inspiration/General Tools

* [PERN Stack Course - PostgreSQL, Express, React, and Node](https://www.youtube.com/watch?v=ldYcgPKEZC8&t=116s)
* [React documentation](https://reactjs.org/docs/getting-started.html)
* [Enable Emmet support for JSX in Visual Studio Code | React](https://medium.com/@eshwaren/enable-emmet-support-for-jsx-in-visual-studio-code-react-f1f5dfe8809c)
* [js-beautify for VS Code](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)

## Contact

Repo created by [ABateman](https://www.andrewbateman.org) - feel free to contact me!
