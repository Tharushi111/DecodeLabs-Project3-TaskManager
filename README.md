<div align="center">
  <h1>Task Manager API</h1>
  <p><strong>DecodeLabs Internship — Project 3: Database Integration</strong></p>
  <p>
    <a href="#-technologies">Technologies</a> •
    <a href="#-api-endpoints">API Endpoints</a> •
    <a href="#-setup-instructions">Setup</a> •
    <a href="#-database-schema">Database Schema</a> •
    <a href="#-author">Author</a>
  </p>
  <br>
</div>

---

## Project Overview

This is **Project 3** of my Full Stack Development internship at **DecodeLabs**. The task was to build a **Spring Boot REST API** with **PostgreSQL database integration** performing full **CRUD (Create, Read, Update, Delete)** operations.

The API manages tasks with fields for title, description, completion status, and automatic timestamps.

---

## Project Requirements Met

| Requirement | Implementation |
|-------------|----------------|
| **Database Integration** | PostgreSQL with Spring Data JPA |
| **CRUD Operations** | Create, Read, Update, Delete via REST endpoints |
| **Proper Data Handling** | Validation, error handling, HTTP status codes |
| **RESTful Standards** | Proper HTTP methods and status codes |
| **Parameterized Queries** | JPA handles SQL injection protection |
| **Database Constraints** | NOT NULL, UNIQUE, validation annotations |

---

## Technologies

| Category | Technologies |
|----------|--------------|
| **Framework** | Spring Boot 3.4.x |
| **ORM** | Spring Data JPA (Hibernate) |
| **Database** | PostgreSQL 18 |
| **Build Tool** | Maven |
| **Language** | Java 17 |
| **Lombok** | Reduces boilerplate code |
| **Validation** | Jakarta Validation API |

---

## API Endpoints

| Method | Endpoint | Description | Request Body |
|--------|----------|-------------|--------------|
| **POST** | `/api/tasks` | Create a new task |  Yes |
| **GET** | `/api/tasks` | Get all tasks |  No |
| **GET** | `/api/tasks/{id}` | Get task by ID |  No |
| **GET** | `/api/tasks/status?completed=true` | Get tasks by status |  No |
| **PUT** | `/api/tasks/{id}` | Update a task |  Yes |
| **DELETE** | `/api/tasks/{id}` | Delete a task |  No |
| **DELETE** | `/api/tasks` | Delete all tasks |  No |

---

##  Request & Response Examples

###  Create a Task (POST)

**Request:**
```http
POST /api/tasks
Content-Type: application/json

{
    "title": "Learn Spring Boot",
    "description": "Complete Project 3 for DecodeLabs",
    "completed": false
}
```

**Response (201 Created):**
```json
{
    "id": 1,
    "title": "Learn Spring Boot",
    "description": "Complete Project 3 for DecodeLabs",
    "completed": false,
    "createdAt": "2026-06-21T20:15:00",
    "updatedAt": "2026-06-21T20:15:00"
}
```

---

###  Get All Tasks (GET)

**Request:**
```http
GET /api/tasks
```

**Response (200 OK):**
```json
[
    {
        "id": 1,
        "title": "Learn Spring Boot",
        "description": "Complete Project 3 for DecodeLabs",
        "completed": false,
        "createdAt": "2026-06-21T20:15:00",
        "updatedAt": "2026-06-21T20:15:00"
    },
    {
        "id": 2,
        "title": "Master PostgreSQL",
        "description": "Learn database integration and CRUD",
        "completed": true,
        "createdAt": "2026-06-21T20:16:00",
        "updatedAt": "2026-06-21T20:17:00"
    }
]
```

---

###  Get Task by ID (GET)

**Request:**
```http
GET /api/tasks/1
```

**Response (200 OK):**
```json
{
    "id": 1,
    "title": "Learn Spring Boot",
    "description": "Complete Project 3 for DecodeLabs",
    "completed": false,
    "createdAt": "2026-06-21T20:15:00",
    "updatedAt": "2026-06-21T20:15:00"
}
```

**Error (404 Not Found):**
```json
{
    "timestamp": "2026-06-21T20:20:00",
    "status": 404,
    "error": "Not Found",
    "message": "Task not found with id: 99"
}
```

---

###  Update a Task (PUT)

**Request:**
```http
PUT /api/tasks/1
Content-Type: application/json

{
    "title": "Master Spring Boot",
    "description": "Completed Project 3 successfully!",
    "completed": true
}
```

**Response (200 OK):**
```json
{
    "id": 1,
    "title": "Master Spring Boot",
    "description": "Completed Project 3 successfully!",
    "completed": true,
    "createdAt": "2026-06-21T20:15:00",
    "updatedAt": "2026-06-21T20:18:00"
}
```

---

### Delete a Task (DELETE)

**Request:**
```http
DELETE /api/tasks/1
```

**Response:**
- `204 No Content` (Successful)
- `404 Not Found` (Task doesn't exist)

---

### Get Tasks by Status (GET)

**Request:**
```http
GET /api/tasks/status?completed=true
```

**Response (200 OK):**
```json
[
    {
        "id": 2,
        "title": "Master PostgreSQL",
        "description": "Learn database integration and CRUD",
        "completed": true,
        "createdAt": "2026-06-21T20:16:00",
        "updatedAt": "2026-06-21T20:17:00"
    }
]
```

---

## Database Schema

### Table: `tasks`

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `id` | BIGSERIAL | PRIMARY KEY | Auto-generated unique ID |
| `title` | VARCHAR(100) | NOT NULL | Task title (max 100 chars) |
| `description` | VARCHAR(500) | - | Task description (max 500 chars) |
| `completed` | BOOLEAN | NOT NULL, DEFAULT false | Completion status |
| `created_at` | TIMESTAMP | AUTO | Creation timestamp |
| `updated_at` | TIMESTAMP | AUTO | Last update timestamp |

---

##  Setup Instructions

### Prerequisites

- Java 17 or higher
- PostgreSQL 14+ installed
- Maven (or use included wrapper)
- IntelliJ IDEA / VS Code

---

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/DecodeLabs-Project3-TaskManager.git
cd DecodeLabs-Project3-TaskManager
```

---

### Step 2: Create PostgreSQL Database

**Using pgAdmin 4:**

1. Open pgAdmin 4
2. Right-click on **"Databases"**
3. Select **"Create"** → **"Database"**
4. Name: `taskmanager_db`
5. Owner: `postgres`
6. Click **"Save"**

**OR using SQL:**

```sql
CREATE DATABASE taskmanager_db;
```

---

### Step 3: Configure `application.properties`

Open `src/main/resources/application.properties` and update:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/taskmanager_db
spring.datasource.username=postgres
spring.datasource.password=YOUR_PASSWORD_HERE
```

---

### Step 4: Run the Application

**Using IntelliJ:**
1. Open `TaskmanagerApplication.java`
2. Click the green ▶ icon

**Using Maven:**
```bash
./mvnw spring-boot:run
```

**Using VS Code:**
1. Open `TaskmanagerApplication.java`
2. Click **"Run"** button

---

### Step 5: Test the API

**Using Postman:**
1. Open Postman
2. Send a POST request:
   - URL: `http://localhost:8080/api/tasks`
   - Body: `{"title": "My First Task", "description": "Testing API", "completed": false}`

**Using cURL:**
```bash
curl -X POST http://localhost:8080/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"My First Task","description":"Testing API","completed":false}'
```

---

## Project Structure

```
DecodeLabs-Project3-TaskManager/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── decodetask/
│   │   │           └── taskmanager/
│   │   │               ├── TaskmanagerApplication.java   # Main entry point
│   │   │               ├── Task.java                     # Entity class
│   │   │               ├── TaskRepository.java           # JPA repository
│   │   │               ├── TaskService.java              # Business logic
│   │   │               └── TaskController.java           # REST endpoints
│   │   └── resources/
│   │       └── application.properties                    # Configuration
│   └── test/
│
├── .gitignore                 # Ignored files
├── README.md                  # This file
├── pom.xml                    # Maven dependencies
├── mvnw                       # Maven wrapper (Unix)
└── mvnw.cmd                   # Maven wrapper (Windows)
```

---

## Security Notes

| Security Measure | Implementation |
|------------------|----------------|
| **SQL Injection** | Spring Data JPA uses parameterized queries |
| **Password Protection** | Database credentials in `application.properties` (not hardcoded) |
| **Input Validation** | `@Valid`, `@NotBlank`, `@Size` annotations |
| **Error Handling** | Proper HTTP status codes (404, 400, 500) |

---

## What I Learned

- Designing a relational database schema with proper constraints
- Building RESTful APIs with Spring Boot
- Integrating PostgreSQL with Spring Data JPA
- Performing full CRUD operations
- Using Lombok to reduce boilerplate code
- Implementing input validation
- Handling exceptions gracefully
- Testing APIs with Postman

---
