# To-Do List API

## 📖 Description

To-Do List API เป็น RESTful API ที่พัฒนาโดยใช้ Golang สำหรับจัดการ Task Management (ระบบงานที่ต้องทำ) พร้อมด้วย Basic Authentication Middleware เพื่อจัดการผู้ใช้และงาน

### ✨ Features
- 👤 จัดการผู้ใช้ (สร้างผู้ใช้, เก็บ credentials)
- ✅ จัดการงาน (สร้าง, อัพเดตสถานะ, ลบ)
- 🔍 ดึงรายการงานทั้งหมด พร้อม filter ด้วย status
- 📄 ดึงรายละเอียดงานตาม UID

## 🏗️ API Endpoints

Base Path: /api/v1

| Method | Endpoint          | Description                              | Auth Required |
| ------ | ----------------- | ---------------------------------------- | ------------- |
| POST   | `/users/register` | สมัครสมาชิกใหม่                          | ❌             |
| POST   | `/users/login`    | เข้าสู่ระบบ (คืนค่า token)               | ❌             |
| GET    | `/tasks`          | ดึงรายการ tasks (filter ด้วย status ได้) | ✅             |
| GET    | `/tasks/:uid`      | ดึงรายละเอียด task ตาม `uid`              | ✅             |
| POST   | `/tasks`          | สร้าง task ใหม่                          | ✅             |
| PUT    | `/tasks/:uid`      | อัพเดตสถานะหรือแก้ไขรายละเอียดของ task   | ✅             |
| DELETE | `/tasks/:uid`      | ลบ task ตาม `uid`                         | ✅             |

## ⚙️ Installation

1. Clone repository

```bash
git clone https://github.com/saharuth-nu/todo-api-golang.git
cd todo-api-golang
```

2. ติดตั้ง dependency

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
# TODO: เพิ่มรายละเอียดเช่น DB connection, JWT secret, App port ฯลฯ
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
