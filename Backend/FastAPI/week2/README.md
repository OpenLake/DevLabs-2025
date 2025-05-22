## 📅 Week 2: Authentication, Advanced Features & Deployment

### 🔹 Day 8 — User Authentication Basics & Password Hashing
- Importance of authentication  
- Hash passwords securely with `passlib`

**Task:**  
Create User model and implement password hashing utility functions.

---

### 🔹 Day 9 — JWT Token Authentication Setup
- JWT concepts & FastAPI security utilities  
- Create JWT token generation & verification

**Task:**  
Build `/token` endpoint for user login that returns JWT tokens.  
Protect API routes using JWT authentication.

---

### 🔹 Day 10 — User Registration & Login Endpoints
- User signup & login workflows  
- Return JWT tokens on successful login

**Task:**  
Implement `/register` and `/login` endpoints.  
Test user registration and token-based login.

---

### 🔹 Day 11 — Linking Tasks to Users & Authorization
- Add one-to-many relationship (users → tasks)  
- Ensure users can only access their own tasks

**Task:**  
Modify Task model to include `owner_id`.  
Update CRUD routes to enforce ownership restrictions.

---

### 🔹 Day 12 — Advanced Features: Pagination & Filtering
- Add pagination to task list (`limit` & `skip` query params)  
- Filter tasks by completion status (`is_completed`)

**Task:**  
Implement pagination and filtering in `/tasks` route.  
Test with different query parameters.

---

### 🔹 Day 13 — Error Handling, Logging & Testing
- Improve error messages and add logging  
- Write automated tests with `pytest`

**Task:**  
Add detailed exception handlers and logs.  
Write and run tests for auth and CRUD endpoints.

---

### 🔹 Day 14 — Deployment Prep & Final Push
- Prepare `requirements.txt` and `.env` config  
- Deploy FastAPI app (Railway, Render, or Heroku)  
- Final README update and push to GitHub

**Task:**  
Deploy live Taskify API.  
Test all endpoints on deployed URL.  
Push final code.

---

## ✅ Week 2 Deliverable:
- Fully authenticated Taskify API with JWT-secured user login  
- Users can securely manage their own tasks  
- Pagination, filtering, logging, and tests implemented  
- App deployed and publicly accessible  

---

