# To-Do List API

## 📖 Description

To-Do List API is a RESTful API built with Golang for managing tasks. It comes with Basic Authentication Middleware to handle user registration, login, and secure task management.

### ✨ Features
- 👤 User management (create users, store credentials)
- ✅ Task management (create, update status, delete)
- 🔍 Retrieve a list of tasks with optional status filter
- 📄 Get detailed information for each task by UID

## 🏗️ API Endpoints

Base Path: /api/v1

| Method | Endpoint          | Description                              | Auth Required |
| ------ | ----------------- | ---------------------------------------- | ------------- |
| POST   | `/users/register` | Register a new user                      | ❌             |
| POST   | `/users/login`    | Login (returns an authentication token)  | ❌             |
| GET    | `/tasks`          | Get all tasks (can filter by status)     | ✅             |
| GET    | `/tasks/:uid`      | Get task details by `uid`               | ✅             |
| POST   | `/tasks`          | Create a new task                        | ✅             |
| PUT    | `/tasks/:uid`      | Update a task’s status or details       | ✅             |
| DELETE | `/tasks/:uid`      | Delete a task by `uid`                  | ✅             |

## ⚙️ Installation

1. Clone repository

```bash
git clone https://github.com/saharuth-nu/todo-api-golang.git
cd todo-api-golang
```

2. Install dependencies

```bash
go mod tidy
```

3. Run server

```bash
go run cmd/server/main.go
```

## 📌 Usage

### Register User

```bash
curl -X POST http://localhost:8080/api/v1/users/register \
-H "Content-Type: application/json" \
-d '{"username":"john","password":"secret"}'
```

### Login User

```bash
curl -X POST http://localhost:8080/api/v1/users/login \
-H "Content-Type: application/json" \
-d '{"username":"john","password":"secret"}'
```

**Response:**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR..."
}
```

### Create Task

```bash
curl -X POST http://localhost:8080/api/v1/tasks \
-H "Authorization: Bearer <your_token>" \
-H "Content-Type: application/json" \
-d '{"title":"Write README","status":"pending"}'
```


## 🔑 Environment Variables

สร้างไฟล์ .env ที่ root ของโปรเจค

```env
# Example environment variables
# TODO: Add details such as DB connection, JWT secret, App port, etc.
PORT=8080
DB_HOST=
DB_PORT=
DB_USER=
DB_PASSWORD=
DB_NAME=
JWT_SECRET=
```

## 📂 Project Structure

```plaintext
personal-blog-api/
├── cmd/
│   └── server/
│       └── main.go         # Entry point
├── config/
│   ├── database            # Database Configuration
│   ├── environment         # Environment Project
├── core/
│   ├── handlers/           # Controllers / Handlers
│   ├── models/             # Database models
│   ├── repositories/       # Data access logic
│   └── services/           # Business logic
├── utils/                  # Utilities / helpers
│   ├── response            # Http Response
├── go.mod
├── go.sum
└── README.md
```
