# Student Management System

A full-stack school management application built with React, Node.js, and PostgreSQL.

## What Was Fixed

**`backend/src/modules/students/students-controller.js`**

All five CRUD handler functions were empty stubs. Implemented:

- `handleGetAllStudents` — fetches students with optional filters (name, class, section, roll)
- `handleAddStudent` — creates a new student and sends a verification email
- `handleGetStudentDetail` — returns full profile for a single student by ID
- `handleUpdateStudent` — updates student details by ID
- `handleStudentStatus` — enables/disables student system access

## Setup

**Prerequisites:** Node.js v16+, PostgreSQL v12+

```bash
# Database
createdb school_mgmt
psql -d school_mgmt -f seed_db/tables.sql
psql -d school_mgmt -f seed_db/seed-db.sql

# Backend
cd backend
npm install
cp .env.example .env   # fill in your DB credentials and secrets
npm start

# Frontend
cd frontend
npm install
npm run dev
```

- Frontend: http://localhost:5173
- Backend API: http://localhost:5007

Demo login — Email: `admin@school-admin.com` / Password: `3OU4zn3q6Zh9`

## Testing the Student Endpoints

Use Postman or curl. All routes require a valid JWT (login first to get the token).

**Login**
```bash
curl -X POST http://localhost:5007/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@school-admin.com","password":"3OU4zn3q6Zh9"}'
```

**List students** (supports `?name=&className=&section=&roll=`)
```bash
curl http://localhost:5007/api/v1/students \
  -H "Authorization: Bearer <token>"
```

**Get student detail**
```bash
curl http://localhost:5007/api/v1/students/:id \
  -H "Authorization: Bearer <token>"
```

**Create student**
```bash
curl -X POST http://localhost:5007/api/v1/students \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{ ...student payload... }'
```

**Update student**
```bash
curl -X PUT http://localhost:5007/api/v1/students/:id \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{ ...updated fields... }'
```

**Toggle student status**
```bash
curl -X POST http://localhost:5007/api/v1/students/:id/status \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{"status": true}'
```
