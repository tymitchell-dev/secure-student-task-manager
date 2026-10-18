# Secure Student Task Manager (SSTM)

## Overview

The **Secure Student Task Manager (SSTM)** is a security-focused web application designed to help students organize academic tasks, manage courses, track deadlines, and monitor their progress. The project combines a Java Spring Boot backend, a MySQL database, and an HTML, CSS, and JavaScript dashboard.

SSTM emphasizes secure authentication, user-specific data access, task-to-course relationships, and reliable database operations.

## Features

### Authentication and Security
- User registration and login
- BCrypt password hashing
- Session-based authentication and logout
- Protected dashboard access
- User-specific task and course access
- Validation of user ownership when managing records

### Task Management
- Create, view, update, and delete tasks
- Associate tasks with courses
- Track task status and priority
- Manage due dates and descriptions
- Filter and sort tasks
- Identify overdue and upcoming tasks
- Automatically update dashboard statistics

### Course Management
- Create and manage courses
- Store course names, instructors, and semesters
- Edit and delete courses
- Associate tasks with their corresponding courses

### Dashboard
- Display total, pending, completed, and overdue tasks
- Show overall task completion progress
- View and manage tasks and courses
- Refresh data from the backend
- Maintain task and course data through MySQL persistence

### Notifications
- Store notification records in MySQL
- Associate notifications with users and tasks
- Track notification types, messages, read status, reminder keys, and creation timestamps
- Handle notification records when deleting associated tasks to maintain database consistency

## Technologies Used

| Component | Technology |
|---|---|
| Backend | Java, Spring Boot |
| Security | Spring Security, BCrypt |
| Database | MySQL |
| Database Access | Spring Data JPA, Hibernate |
| Build Tool | Maven |
| Frontend | HTML, CSS, JavaScript |
| API Testing | Thunder Client |
| Database Management | MySQL Workbench |
| Development Environment | Visual Studio Code |
| Version Control | Git and GitHub |
| Design and Documentation | Draw.io |

## Project Structure

The repository contains frontend, backend, database documentation, and project documentation.

```text
SSTM/
├── frontend/
│   └── index.html
├── backend/
│   ├── database/
│   │   ├── docs/
│   │   │   ├── diagrams/
│   │   │   ├── screenshots/
│   │   │   └── wireframes/
│   │   └── index.html
│   └── index.html
├── index.html
└── README.md
```

The Spring Boot application's Java source code is organized using a layered architecture:

```text
src/main/java/com/sstm/sstm/
├── config/
├── controller/
├── model/
├── repository/
└── service/
```

- **config:** Application and security configuration.
- **controller:** HTTP endpoints and request handling.
- **model:** Entity classes representing users, tasks, and courses.
- **repository:** Database access through Spring Data JPA.
- **service:** Business logic and application operations.

The main Spring Boot application and configuration files are maintained within the backend project.

## System Functionality

### Authentication

Users can register and log in to access their accounts. Passwords are hashed with BCrypt before storage. Protected pages require an authenticated session, and logging out returns users to the login page.

### Task Management

Tasks support the following information:

- Title and description
- Status, including pending and completed
- Priority: LOW, MEDIUM, or HIGH
- Due date
- Associated user
- Associated course

Users can create, view, update, and delete their tasks. The application checks record ownership to help prevent users from accessing another account's tasks.

### Course Management

Courses store information such as:

- Course name
- Instructor
- Semester

Users can create and manage courses and associate tasks with the appropriate course.

### Dashboard and Progress Tracking

The dashboard retrieves application data from the backend and presents task statistics, completion progress, and task information. Statistics are calculated from the stored task data rather than existing only in the browser.

### Notifications and Database Consistency

The database includes notification records associated with tasks and users. When a task is deleted, its associated notification records are handled before the task record is removed to avoid the foreign-key constraint error encountered during development.

## API Endpoints

The following are the intended REST API routes. Authentication routes and security behavior should be verified against the current controller and security configuration.

### Authentication

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/auth/register` | Register a user |
| POST | `/auth/login` | Authenticate a user |
| POST | `/logout` | End the authenticated session |

### Tasks

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/tasks` | Create a task |
| GET | `/api/tasks` | Retrieve the authenticated user's tasks |
| GET | `/api/tasks/{id}` | Retrieve a specific task |
| PUT | `/api/tasks/{id}` | Update a task |
| DELETE | `/api/tasks/{id}` | Delete a task |

### Courses

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/courses` | Create a course |
| GET | `/api/courses` | Retrieve the authenticated user's courses |
| GET | `/api/courses/{id}` | Retrieve a specific course |
| PUT | `/api/courses/{id}` | Update a course |
| DELETE | `/api/courses/{id}` | Delete a course |

**Note:** Confirm the exact authentication paths and available single-record endpoints against the current implementation before treating this table as a complete API reference. Spring Security may also require CSRF tokens for state-changing requests.

## Database Design

SSTM uses MySQL to persist user, task, course, and notification data.

The main relationships include:

- A user can have multiple tasks.
- A user can manage multiple courses.
- A task belongs to a specific user.
- A task can be associated with a course.
- Notifications can reference associated tasks and users.

JPA entities and repositories provide database access, while foreign-key relationships help maintain referential integrity.

## Testing and Verification

Development testing has included API requests, browser-based testing, and database verification.

Verified functionality includes:

- User registration and login
- Password hashing with BCrypt
- Protected dashboard access and logout
- Creating, viewing, editing, and deleting tasks
- Creating and managing courses
- Linking tasks to courses
- Isolating task and course data between user accounts
- Dashboard statistics and progress calculations
- Persistence of application data in MySQL
- Handling associated notifications when deleting tasks

Thunder Client, the browser, PowerShell, and MySQL Workbench have been used during development and troubleshooting.

## Project Progress

### Weeks 1–4: Requirements and Design — Completed
- Gathered requirements and established the product vision.
- Developed user personas, scenarios, and user stories.
- Created the entity-relationship diagram.
- Developed initial UI wireframes.

### Weeks 5–6: Backend Setup and Authentication — Completed
- Initialized the Spring Boot project.
- Configured the MySQL database connection.
- Established the layered backend architecture.
- Created the user model and database integration.
- Implemented registration and BCrypt password hashing.
- Developed authentication and session-handling functionality.

### Week 7: Task Management — Completed
- Created the Task entity and JPA relationships.
- Implemented the task repository, service, and controller.
- Developed task CRUD operations.
- Tested task endpoints and database persistence.

### Weeks 8–9: Course Management and Integration — Completed
- Created the Course entity, repository, service, and controller.
- Connected tasks to users and courses.
- Resolved JSON serialization and database constraint issues.
- Tested course management and integrated task functionality.

### Week 10: Dashboard and Notifications — Implemented
- Connected the dashboard to backend task and course data.
- Added task statistics and progress tracking.
- Implemented task filtering and sorting.
- Added task and course management from the dashboard.
- Tested account-specific data isolation.
- Addressed task deletion errors caused by related notification records.
- Organized screenshots documenting the interface and database.

## Current Status

The core SSTM application is functional, with authentication, task management, course management, dashboard integration, and MySQL persistence implemented and tested. Account isolation and notification-related task deletion have also been verified during development.

Further testing, documentation, and security improvements remain part of the project's ongoing development.

## Next Steps

- Evaluate and implement JWT authentication if required by the project specifications.
- Expand notification and reminder functionality.
- Improve input validation and error handling.
- Add automated tests for authentication, authorization, and CRUD operations.
- Review security configuration, including CSRF protection and session handling.
- Complete technical documentation and organize project screenshots.
- Evaluate deployment options for a test environment.

## Screenshots and Documentation

Project screenshots and design materials are stored under:

`backend/database/docs/`

Recommended contents include:

- `screenshots/` — Login page, dashboard, task management, and notification table.
- `diagrams/` — Entity-relationship and architecture diagrams.
- `wireframes/` — Initial interface designs.

Screenshots provide visual evidence of application functionality and database structure.

## Running the Application Locally

### Prerequisites
- Java 21
- MySQL
- Git
- Internet access for the initial Maven dependency download

### Steps

1. Clone the repository:

   ```bash
   git clone <your-github-repository-url>
   ```

2. Open the Spring Boot backend project directory containing `pom.xml` and `mvnw.cmd`.

3. Configure the database connection in `src/main/resources/application.properties` to match your local MySQL settings. Do not commit database passwords or other secrets.

4. Start MySQL and ensure the configured database exists.

5. Start the application on Windows:

   ```powershell
   .\mvnw.cmd spring-boot:run
   ```

6. Open the login page in your browser:

   `http://localhost:8080/login.html`

The application requires a valid database configuration and the necessary Maven dependencies. Follow the project's current security configuration when testing authenticated API requests.

## Author

**Ty Mitchell**

Secure Student Task Manager (SSTM) — Software Engineering Project
