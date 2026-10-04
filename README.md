# Secure Student Task Manager (SSTM)

## Overview
The Secure Student Task Manager (SSTM) is a secure web-based application designed to help students manage academic tasks, courses, and deadlines efficiently. The system focuses on organization, productivity, and secure data handling through a structured backend architecture and modern development practices.



## Features
- User authentication (registration and login)
- Secure password encryption using BCrypt
- Task management (Create, Read, Update, Delete)
- Course management (Create, Read, Update, Delete)
- Task-to-course relationship
- Secure data validation and persistence
- RESTful API design for scalability



## Technologies Used
- **Backend:** Java (Spring Boot)
- **Security:** Spring Security, BCrypt
- **Database:** MySQL
- **Build Tool:** Maven
- **Testing Tool:** Thunder Client
- **Frontend (Planned):** HTML, CSS, JavaScript



## Project Structure
src/main/java/com/sstm/sstm
│── config # Security configuration
│── controller # REST API endpoints
│── model # Entity classes (User, Task, Course)
│── repository # Database access layer
│── service # Business logic


## System Functionality

### Authentication
- Users can register and log in securely
- Passwords are hashed using BCrypt before storage
- User data is protected and validated

### Task Management
- Create, view, update, and delete tasks
- Each task includes:
  - Title
  - Description
  - Status (PENDING / COMPLETED)
  - Priority (LOW / MEDIUM / HIGH)
  - Due date

### Course Management
- Create and manage courses
- Each course includes:
  - Name
  - Instructor
  - Semester

### Relationships
- Each task is linked to:
  - A specific user
  - A specific course
- Ensures structured and organized data tracking



## API Endpoints

### Authentication
- POST /api/auth/register – Register user
- POST /api/auth/login – Login user

### Tasks
- POST /api/tasks – Create task
- GET /api/tasks – Get all tasks
- GET /api/tasks/{id} – Get task by ID
- PUT /api/tasks/{id} – Update task
- DELETE /api/tasks/{id} – Delete task

### Courses
- POST /api/courses – Create course
- GET /api/courses – Get all courses
- GET /api/courses/{id} – Get course by ID
- PUT /api/courses/{id} – Update course
- DELETE /api/courses/{id} – Delete course



## Testing

The application was tested using Thunder Client with successful responses for:

- User registration
- Course creation
- Task creation (linked to user and course)
- Retrieval of all tasks and courses

All endpoints returned valid JSON responses and were successfully stored in the MySQL database.



## Progress

### Weeks 1–4 (Completed)
- Requirements gathering
- System design and planning
- ER Diagram creation
- UI wireframes

### Weeks 5–6 (Completed)
- Initialized Spring Boot backend project
- Configured MySQL database connection
- Implemented layered architecture
- Created User entity and database integration
- Implemented user registration with validation
- Added secure password hashing (BCrypt)
- Began authentication system

### Week 7 (Completed)
- Implemented Task entity with JPA relationships
- Created TaskRepository, TaskService, and TaskController
- Developed full CRUD API for tasks
- Tested endpoints using Thunder Client

### Weeks 8–9 (Completed)
- Implemented Course entity and relationships
- Created CourseRepository, CourseService, and CourseController
- Connected tasks to courses and users
- Fixed JSON serialization issues
- Resolved database constraint errors (user_id not null)
- Successfully tested full system integration



## Current Status
The backend system is fully functional and integrated with a MySQL database. Authentication, task management, and course management features are complete and tested. The system demonstrates a secure and scalable architecture using REST APIs.



## Next Steps
- Implement JWT-based authentication
- Develop frontend user interface
- Add notifications and reminders
- Improve validation and error handling
- Deploy application for real-world testing



## Author
**Ty Mitchell**
