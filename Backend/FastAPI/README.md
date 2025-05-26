# 🟢 FastAPI Development Track

## 🛠 Tech Stack

* **Python 3.10+**
* **FastAPI**
* **Uvicorn (ASGI Server)**
* **SQLAlchemy / Tortoise ORM**
* **PostgreSQL / SQLite (as DB)**
* **Pydantic**
* **Postman / Thunder Client (for API testing)**

---

## 📚 Recommended Guides

* [FastAPI Official Docs](https://fastapi.tiangolo.com/)
* [Python Engineer - FastAPI Beginner Tutorial](https://www.youtube.com/watch?v=7t2alSnE2-I)
* [FastAPI Tutorial Series by Sebastián Ramírez](https://fastapi.tiangolo.com/tutorial/)
* [JWT Auth in FastAPI](https://fastapi.tiangolo.com/tutorial/security/)
* [Build a CRUD API with FastAPI and SQLModel](https://sqlmodel.tiangolo.com/tutorial/fastapi/)
* [FastAPI Error Handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)
* [Deploy FastAPI on Render](https://render.com/docs/deploy-fastapi)
* [FastAPI Starter Template (GitHub)](https://github.com/tiangolo/full-stack-fastapi-postgresql)

---

## ✅ Complete Roadmap 

---

### 1. 🧠 Introduction to Git and GitHub

* OpenLake: **GitStartedWithUs**
* YouTube: *Git and GitHub Crash Course*
* Learn version control to manage your projects efficiently.

---

### 2. Environment Setup

**Steps:**

* Install Python 3.10+
* Create and activate a virtual environment  
```bash
python -m venv env
source env/bin/activate  # Linux/Mac
env\Scripts\activate     # Windows
````

* Install FastAPI and Uvicorn

```bash
pip install fastapi uvicorn
```

* Install SQLAlchemy or Tortoise ORM as needed

```bash
pip install sqlalchemy
```

* Set up a new GitHub repository, initialize a project.

**Resources:**

* [FastAPI Installation Guide](https://fastapi.tiangolo.com/#installation)
* [Python Virtual Environments](https://realpython.com/python-virtual-environments-a-primer/)

---

### 3. 📦 FastAPI Fundamentals

**Topics:**

* FastAPI basics: `GET`, `POST`, `PUT`, `DELETE`
* Path parameters & query parameters
* Request body using Pydantic models
* Response models & status codes
* Running server with Uvicorn

**Resources:**

* [FastAPI Docs - Tutorial](https://fastapi.tiangolo.com/tutorial/)
* [FastAPI Crash Course](https://www.youtube.com/watch?v=7t2alSnE2-I)

---

### 4. 🚀 Building API Routes

**Topics:**

* Create routes for resources like Tasks, Users, Auth
* Organize code using `routers`
* Middleware basics
* Error handling and custom exceptions

**Resources:**

* [FastAPI Routing](https://fastapi.tiangolo.com/tutorial/bigger-applications/)
* [FastAPI Error Handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

---

### 5. 🔁 REST API Development

**Topics:**

* RESTful API principles (CRUD)
* CRUD operations for Task Manager
* Use SQLite/PostgreSQL with SQLAlchemy
* Organizing models, schemas, and database sessions
* Test APIs using Postman/Thunder Client

**Tools:**

* [Postman](https://www.postman.com/)
* [Thunder Client (VS Code)](https://www.thunderclient.com/)

**Resources:**

* [FastAPI + SQLAlchemy Guide](https://fastapi.tiangolo.com/tutorial/sql-databases/)
* [FastAPI CRUD Video](https://www.youtube.com/watch?v=7t2alSnE2-I)
* [Build a CRUD API with FastAPI and SQLModel](https://sqlmodel.tiangolo.com/tutorial/fastapi/)

---

### 6. 🔐 Authentication & Authorization

**Topics:**

* User registration and login routes
* Password hashing with `passlib`
* JWT token-based authentication
* OAuth2 Password Flow
* Role-based permissions and protecting routes

**Libraries:**

```bash
pip install python-jose passlib[bcrypt]
```

**Resources:**

* [FastAPI JWT Auth Guide](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/)
* [JWT Auth Video](https://www.youtube.com/watch?v=7t2alSnE2-I&t=2300s)
* [JWT Auth in FastAPI](https://fastapi.tiangolo.com/tutorial/security/)

---

### 7. 🌐 Database Integration

**Topics:**

* Connect FastAPI with SQLite/PostgreSQL
* Define models using SQLAlchemy or Tortoise ORM
* Establish database sessions
* Migrate and seed database

**Libraries:**

```bash
pip install sqlalchemy psycopg2-binary alembic
```

**Resources:**

* [SQLAlchemy Docs](https://docs.sqlalchemy.org/en/20/)
* [Alembic Docs](https://alembic.sqlalchemy.org/en/latest/)
* [FastAPI + SQLAlchemy Full Tutorial](https://www.youtube.com/watch?v=7t2alSnE2-I)

---

### 8. 🧪 Validation & Error Handling

**Topics:**

* Validate incoming data using Pydantic models
* Set default values and constraints
* Create custom exceptions and error handlers
* Use dependency injections for validation
* Global error handling middleware

**Resources:**

* [FastAPI Validation Docs](https://fastapi.tiangolo.com/tutorial/body/)
* [Error Handling Tutorial](https://fastapi.tiangolo.com/tutorial/handling-errors/)

### 9. Boilerplate & Example Projects
- [FastAPI Starter Template (GitHub)](https://github.com/tiangolo/full-stack-fastapi-postgresql)


---

> 💡 *Practice everything incrementally and by the end you’ll have a fully working backend with Auth, CRUD, and database integration using FastAPI! 🚀*

