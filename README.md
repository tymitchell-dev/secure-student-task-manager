Secure Student Task Manager (SSTM)

Overview
The Secure Student Task Manager (SSTM) is a secure web-based application designed to help students manage academic tasks, courses, and deadlines efficiently. The system emphasizes organization, productivity, and secure data handling through a well-structured backend architecture and modern development practices.

Features
User authentication (registration and login)
Secure password encryption using BCrypt
Task management (create, read, update, delete)
Course organization (in progress)
Notifications and reminders (planned)
Secure data handling and validation
RESTful API design for scalability

Technologies
Backend: Java (Spring Boot)
Security: Spring Security, BCrypt
Database: MySQL
Build Tool: Maven
Frontend (Planned): HTML, CSS, JavaScript

Project Structure
src/main/java/com/sstm/sstm
│── config       # Security configuration
│── controller   # REST API endpoints
│── model        # Entity classes
│── repository   # Database layer
│── service      # Business logic

Progress
Weeks 1–4 (Completed)
Requirements gathering
System design and planning
ER Diagram creation
UI wireframes
Weeks 5–6 (Completed)
Initialized Spring Boot backend project
Configured MySQL database connection
Implemented layered architecture (Controller, Service, Repository, Model)
Created User entity and integrated database using JPA
Implemented user registration with validation
Added secure password hashing using BCrypt
Began authentication system (login functionality)
Week 7 (Completed)
Implemented Task entity with JPA annotations
Created TaskRepository using Spring Data JPA
Developed TaskService for business logic
Built TaskController with full REST API endpoints
Successfully tested API using Thunder Client:
POST (Create Task)
GET (All Tasks)
GET (Task by ID)
PUT (Update Task)
DELETE (Remove Task)
Verified full CRUD functionality with MySQL database integration

Current Status
The backend system is fully functional and connected to a MySQL database. Core authentication features are implemented, and task management functionality has been successfully developed and tested using REST API endpoints. The application now supports full CRUD operations for tasks, demonstrating a working backend system with proper architecture, security practices, and database integration.

Next Steps
Implement course management functionality
Improve authentication with JWT-based security
Develop frontend user interface
Add notifications and reminders
Enhance validation and error handling
Deploy application for testing

Author
Ty Mitchell
B.S. Computer Science – University of North Georgia
Concentration: Information Assurance and Security (IAS)
