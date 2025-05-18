## 🌱 Node.js & Express.js Learning Track for Taskify

A step-by-step guide to get started with backend development using **Node.js** and **Express.js**.

---

### ✅ Step 1: Understand Node.js Basics

#### 📚 Topics:

* What is Node.js?
* Installing Node.js & npm
* Running JavaScript with Node
* `console.log`, `require`, `module.exports`
* Understanding `package.json`

#### 🛠️ Practice:

* Create and run a `hello.js` file with `console.log("Hello Node")`
* Initialize a project with `npm init -y`

#### 🔗 Resources:

* [Node.js Official Docs](https://nodejs.org/en/docs)
* [Node.js Crash Course (YouTube)](https://www.youtube.com/watch?v=fBNz5xF-Kx4)

---

### ✅ Step 2: Introduction to Express.js

#### 📚 Topics:

* What is Express.js?
* Installing Express
* Creating a basic Express server
* Handling routes (`GET`, `POST`)
* Sending JSON response

#### 🛠️ Practice:

* Create an Express server
* Add `/`, `/about`, and `/contact` routes

#### 🔗 Resources:

* [Express.js Docs](https://expressjs.com/)
* [Express Crash Course – Traversy Media](https://www.youtube.com/watch?v=L72fhGm1tfE)

---

### ✅ Step 3: Creating a Simple REST API

#### 📚 Topics:

* REST API basics (GET, POST, PUT, DELETE)
* Using `req.body`, `req.params`, `req.query`
* Basic CRUD operations using arrays

#### 🛠️ Practice:

* Create a "Books" API with routes:

  * `GET /books`
  * `GET /books/:id`
  * `POST /books`
  * `PUT /books/:id`
  * `DELETE /books/:id`

#### 🔗 Tools:

* [Thunder Client (VS Code Extension)](https://www.thunderclient.com/)
* [Postman](https://www.postman.com/)

#### 🔗 Resources:

* [Express.js routing guide](https://expressjs.com/en/guide/routing.html)

---

### ✅ Step 4: Middleware & Static Files

#### 📚 Topics:

* What is middleware?
* Using built-in middleware (`express.json()`, `express.static`)
* Creating custom middleware

#### 🛠️ Practice:

* Create a custom middleware to log time and URL
* Serve static HTML files from a `public` folder

---

### ✅ Step 5: Build an Authentication Service (Login & Signup)

#### 📚 Topics:

* What is authentication & authorization
* Password hashing using `bcrypt`
* JSON Web Tokens (JWT)
* Protecting private routes
* Token-based user sessions

#### 🛠️ Practice:

* Create `POST /register` and `POST /login` routes
* Store user data (can use in-memory or simple JSON file)
* Use `bcrypt` to hash passwords before storing
* Use `jsonwebtoken` to generate a token during login
* Create a middleware to verify the token and protect routes like `GET /profile`

#### 📦 Libraries:

```bash
npm install bcrypt jsonwebtoken
```

#### 🔐 Folder Structure Suggestion:

```
auth-app/
├── controllers/
│   └── authController.js
├── routes/
│   └── authRoutes.js
├── middleware/
│   └── authMiddleware.js
├── app.js
└── users.json  (or in-memory array for storing user data)
```

#### 🔗 Resources:

* [JWT Crash Course – Traversy Media](https://www.youtube.com/watch?v=mbsmsi7l3r4)
* [bcrypt Documentation](https://www.npmjs.com/package/bcrypt)
* [jsonwebtoken Docs](https://github.com/auth0/node-jsonwebtoken)

---

### ✅ Step 6: Simple Project (Capstone)

#### 💡 Project Idea:

**Task Manager API**
Features:

* Add a task
* View all tasks
* Update a task
* Delete a task

---

### 🧑‍🎓 After Completing This Track, You Will:

* Understand how Node.js and Express.js work
* Be able to build and test basic APIs
* Be ready to move to MongoDB integration and authentication
