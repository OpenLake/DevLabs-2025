# 🟢 DevLabs FastAPI Backend Track — 2-Week Plan for Taskify 🚀

Welcome to **the 2-week FastAPI Backend Development Journey by OpenLake!**  
Build a fully functional Taskify REST API app — with CRUD, auth, database, validation, error handling, and deployment.

---

## 📅 Week 1: FastAPI Basics + CRUD + Database Integration

### 🔹 Day 1 — Introduction & Environment Setup
- What is FastAPI & why use it?  
- Install Python 3.10+ & create a virtual environment  
- Install FastAPI and Uvicorn  
- Build & run a simple “Hello, Taskify!” FastAPI server

**Task:**  
Set up the environment and run your first FastAPI app.

---

### 🔹 Day 2 — API Routes & Endpoints Basics
- Understand HTTP methods & API endpoints  
- Path and query parameters  
- Test APIs with Thunder Client / Postman

**Task:**  
Create `/tasks` GET route returning a hardcoded list.  
Add POST, PUT, DELETE routes with path parameters and test all.

---

### 🔹 Day 3 — Pydantic Models & Validation
- Define request & response models with Pydantic  
- Validate input data types and constraints

**Task:**  
Create Pydantic models for tasks (e.g., `TaskCreate`, `Task`).  
Implement POST `/tasks` to accept validated input JSON.

---

### 🔹 Day 4 — Implement Full CRUD Operations
- Organize project with routers and schemas  
- Build CRUD routes (`GET`, `POST`, `PUT`, `DELETE`)

**Task:**  
Complete all CRUD endpoints for Task manager.  
Test routes end-to-end with sample data.

---

### 🔹 Day 5 — PostgreSQL Setup & Database Connection

- Install PostgreSQL locally or use a cloud service (Railway, Supabase, ElephantSQL)
- Install Python dependencies:
  ```bash
  pip install psycopg2 python-dotenv
  ```

- Create a `.env` file to store your database credentials:
  ```
  DATABASE_URL=postgresql://username:password@localhost:5432/taskify_db
  ```

- Create a `database.py` file to manage your PostgreSQL connection:
  ```python
  import psycopg2
  from dotenv import load_dotenv
  import os

  load_dotenv()

  DATABASE_URL = os.getenv("DATABASE_URL")

  def get_connection():
      conn = psycopg2.connect(DATABASE_URL)
      return conn
  ```

- Create your `tasks` table directly using SQL:
  ```sql
  CREATE TABLE tasks (
      id SERIAL PRIMARY KEY,
      title TEXT NOT NULL,
      is_completed BOOLEAN DEFAULT FALSE
  );
  ```

**Task:**  
✅ Configure your PostgreSQL database connection and manually create the `tasks` table via SQL query.

---

### 🔹 Day 6 — Integrating FastAPI CRUD with PostgreSQL

- Use `psycopg2` to interact with PostgreSQL in your route functions
- For each CRUD operation:
  - Open a connection using `get_connection()`
  - Create a cursor
  - Execute raw SQL queries
  - Commit changes if needed
  - Close the connection

**Example:** `GET /tasks`
```python
from fastapi import APIRouter
from database import get_connection

router = APIRouter()

@router.get("/tasks")
def get_tasks():
    conn = get_connection()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM tasks")
    tasks = cursor.fetchall()
    conn.close()
    return {"tasks": tasks}
```

**Task:**  
✅ Implement full CRUD operations (Create, Read, Update, Delete) for your `tasks` table using direct PostgreSQL queries inside your FastAPI routes.

✅ Test endpoints with Thunder Client or Postman.

---

> 💡 *Pro Tip: Start by testing SELECT and INSERT queries first before adding UPDATE and DELETE.*


### 🔹 Day 7 — Validation, Error Handling & GitHub Push
- Add advanced validation constraints  
- Implement exception handling with HTTP errors  
- Initialize git repo and push code to GitHub

**Task:**  
Add 404 for missing tasks.  
Commit and push your working Week 1 code.

---

## ✅ Week 1 Deliverable:
- FastAPI Task Manager API with SQLite-backed CRUD  
- Validated input, error handling, and clean project structure  
- Code hosted on GitHub repository

---
