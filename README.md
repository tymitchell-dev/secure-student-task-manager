# Secure Student Task Manager (SSTM)

## Overview

The **Secure Student Task Manager (SSTM)** is a security-focused web application designed to help students organize academic tasks, manage courses, track deadlines, and monitor their progress. The application combines a Java Spring Boot backend, a MySQL database, and an HTML, CSS, and JavaScript frontend.

SSTM emphasizes secure authentication, user-specific data access, input validation, database integrity, and reliable task and notification management.

## Features

### Authentication and Security

- User registration and login.
- BCrypt password hashing.
- Session-based authentication and logout.
- Protected application resources.
- User-specific task and course access.
- Ownership checks for record retrieval, modification, and deletion.
- Input validation for task and course data.
- CSRF protection for applicable state-changing requests.
- Configured session timeout.
- Restricted database account permissions.
- Error handling that avoids exposing stack traces.

### Task Management

- Create, view, update, and delete tasks.
- Associate tasks with courses.
- Track task status and priority.
- Store due dates and descriptions.
- Filter and sort tasks.
- Identify overdue and upcoming tasks.
- Validate task titles, descriptions, priorities, and statuses.
- Maintain task data in MySQL.

### Course Management

- Create and manage courses.
- Store course names, instructors, and semesters.
- Edit and delete courses.
- Associate tasks with their corresponding courses.
- Validate course information.
- Restrict course operations to authorized users.

### Dashboard

- Display task statistics.
- Track pending and completed tasks.
- Display task completion progress.
- View and manage tasks and courses.
- Retrieve application data from the backend.
- Maintain persistent data through MySQL.

### Notifications and Reminders

- Store notification records in MySQL.
- Associate notifications with users and tasks.
- Track notification types, messages, read status, reminder keys, and creation timestamps.
- Support automatic task reminder processing.
- Prevent duplicate reminders through stable reminder identifiers.
- Handle notification records associated with deleted tasks to maintain database consistency.

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

The repository contains frontend files, backend resources, database documentation, and project documentation.

SSTM/
├── frontend/
│   └── index.html
├── backend/
│   ├── database/
│   │   └── docs/
│   │       ├── diagrams/
│   │       ├── screenshots/
│   │       └── wireframes/
│   └── index.html
├── index.html
└── README.md

The Spring Boot application's Java source code uses a layered architecture:

src/main/java/com/sstm/sstm/
├── config/
├── controller/
├── dto/
├── exception/
├── model/
├── repository/
└── service/

Each package has a specific responsibility:

- **config:** Contains application settings and security configuration.
- **controller:** Handles HTTP requests, coordinates application operations, and returns API responses.
- **dto:** Contains Data Transfer Objects (DTOs) that define the data exchanged between the frontend and backend. DTOs help control which fields are accepted in requests and returned in responses.
- **exception:** Handles application and API exceptions and provides standardized error responses.
- **model:** Contains entity classes representing users, tasks, courses, and notifications.
- **repository:** Provides database access through Spring Data JPA and Hibernate.
- **service:** Implements business logic, input validation, and application operations.

This layered architecture separates request handling, data transfer, database operations, and business logic, making the application easier to maintain and extend.

The main Spring Boot application and its configuration files are maintained within the backend project.


## System Functionality

### Authentication

Users can register and log in to access their accounts. Passwords are hashed using BCrypt before storage. Protected resources require authentication, and session management controls access to the application.

The application also uses CSRF protection for applicable state-changing requests. Session expiration and logout behavior have been checked during development.

### Task Management

Tasks support the following information:

- Title and description.
- Status, including pending, in-progress, and completed states.
- Priority: LOW, MEDIUM, or HIGH.
- Due date.
- Associated user.
- Associated course.

Users can create, view, update, and delete their tasks. The application validates task information and checks record ownership to help prevent unauthorized access to another user's tasks.

### Course Management

Courses store information such as:

- Course name.
- Instructor.
- Semester.

Users can create and manage their courses and associate tasks with the appropriate course. Course operations include input validation and ownership checks.

### Dashboard and Progress Tracking

The dashboard retrieves application data from the backend and displays task statistics, completion progress, and task information. Statistics are based on stored task data rather than existing only in the browser.

The dashboard, task functionality, and course functionality were checked again after the latest security changes.

### Notifications and Database Consistency

The application stores notification records associated with users and tasks. Automatic reminder processing checks eligible tasks and generates notifications according to the reminder rules.

When a task is deleted, its associated notification records are handled before the task record is removed. This prevents the foreign-key constraint issue encountered during development.

The notification system also uses reminder identifiers to help prevent duplicate notifications.

## API Endpoints

The following tables describe the documented REST API routes. Confirm the exact routes and behavior against the current controller and security configuration.

### Authentication

| Method | Endpoint | Purpose |
|---|---|---|
| POST | /auth/register | Register a user |
| POST | /auth/login | Authenticate a user |
| POST | /logout | End the authenticated session |

### Tasks

| Method | Endpoint | Purpose |
|---|---|---|
| POST | /api/tasks | Create a task |
| GET | /api/tasks | Retrieve the authenticated user's tasks |
| GET | /api/tasks/{id} | Retrieve a specific authorized task |
| PUT | /api/tasks/{id} | Update a specific authorized task |
| DELETE | /api/tasks/{id} | Delete a specific authorized task |

### Courses

| Method | Endpoint | Purpose |
|---|---|---|
| POST | /api/courses | Create a course |
| GET | /api/courses | Retrieve the authenticated user's courses |
| GET | /api/courses/{id} | Retrieve a specific authorized course |
| PUT | /api/courses/{id} | Update a specific authorized course |
| DELETE | /api/courses/{id} | Delete a specific authorized course |


## Database Design

SSTM uses MySQL to persist user, task, course, and notification data.

The main relationships include:

- A user can have multiple tasks.
- A user can manage multiple courses.
- Each task belongs to a specific user.
- A task can be associated with a course.
- Notifications can reference users and associated tasks.

JPA entities and repositories provide database access, while foreign-key relationships help maintain referential integrity.

The application uses a dedicated database account with permissions scoped to the SSTM database rather than relying on a database administrator account for routine application operations.

Database credentials must remain private and should not be committed to the repository.

## Security Testing and Verification

Security and functional verification included manual API requests, browser-based testing, PowerShell commands, and MySQL Workbench.

### Input Validation

The following cases were tested:

- Invalid task priorities.
- Invalid task statuses.
- Blank task titles.
- Task descriptions exceeding the configured length.
- Blank course names.
- Course names, instructor names, and semester values exceeding their configured length limits.

The tested invalid inputs were rejected with HTTP 400 responses.

### XSS and SQL Injection Input Handling

Basic tests were performed using script-like task titles and SQL injection-style text.

The tested script-like input was displayed as literal text without executing the script. The SQL injection-style text was stored literally rather than changing the intended database query.

These checks provide evidence about the tested inputs but do not constitute a comprehensive security assessment.

### Authentication and Authorization

Testing verified that:

- Unauthenticated requests to protected APIs were denied.
- Users could retrieve their own tasks and courses.
- Attempts to access or modify another user's tasks and courses were rejected.
- Requests without the required CSRF token were denied.
- The configured session timeout was enforced during testing.

### Database and API Security

Additional checks verified that:

- The application connected using the restricted `sstm_app` database account.
- The account's permissions were scoped to the SSTM database.
- API responses contained the expected task and course fields.
- Invalid requests returned appropriate error responses.
- Error responses did not expose stack traces.
- SQL logging was disabled in the application configuration.

### Final Regression Testing

After the security changes, the following application features were checked again:

| Feature | Result |
|---|---|
| Dashboard loading and display | Passed |
| Existing task display | Passed |
| Existing course display | Passed |
| Notifications page and existing notifications | Passed |

All four final regression checks passed.

**Testing limitation:** These results document manual checks performed during development. Maven previously reported that no automated tests were available. Automated security testing, comprehensive penetration testing, and complete coverage of all possible inputs and attack scenarios have not been established by these results.

## Project Progress

### Weeks 1–4: Requirements and Design — Completed

- Established the product vision and gathered requirements.
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
- Implemented task repositories, services, and controllers.
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
- Added task and course management through the dashboard.
- Tested account-specific data isolation.
- Addressed task deletion errors caused by related notification records.
- Organized screenshots documenting the interface and database.

### Weeks 11–12: Security Improvements and Verification — Substantially Completed

- Added and tested task and course input validation.
- Evaluated XSS and SQL injection input handling.
- Verified authentication and user-specific resource access.
- Tested session timeout behavior.
- Verified CSRF protection for applicable requests.
- Restricted database account permissions.
- Reviewed API response fields and error handling.
- Disabled SQL logging.
- Checked automatic reminder and notification functionality.
- Completed final manual regression checks for the dashboard, tasks, courses, and notifications.

The main implementation and manual verification work for this phase is substantially complete. Remaining work includes maintaining test documentation, confirming project-specific submission requirements, and expanding automated test coverage.

## Current Status

The core SSTM application includes authentication, task management, course management, dashboard integration, MySQL persistence, and notification functionality.

Manual checks have also covered input validation, access control, session management, CSRF protection, database permissions, API responses, and error handling.

The latest regression checks passed for the dashboard, tasks, courses, and notifications. The project is substantially complete for Weeks 11–12, with additional automated testing and documentation improvements remaining.

## Next Steps

- Add automated tests for authentication, authorization, validation, and CRUD operations.
- Expand negative and security-focused test coverage.
- Review the security configuration before deployment.
- Continue improving notification and reminder behavior.
- Maintain technical documentation and organize project screenshots.
- Evaluate deployment options for a test environment.
- Confirm any remaining instructor or capstone-team requirements.

JWT authentication should only be implemented if it is required by the project specifications; the current application uses session-based authentication.

## Screenshots and Documentation

Project screenshots and design materials are intended to be stored under:

backend/database/docs/

Recommended contents include:

- screenshots/ — Login page, dashboard, task management, and notification table.
- diagrams/ — Entity-relationship and architecture diagrams.
- wireframes/ — Initial interface designs.

Screenshots provide visual evidence of application functionality and database structure. Confirm that the referenced files and directories exist in the repository before publishing this documentation.

## Running the Application Locally

### Prerequisites

- Java 21.
- MySQL.
- Git.
- Internet access for the initial Maven dependency download.

### Steps

1. Clone the repository:

   bash
   git clone <https://github.com/tymitchell-dev/secure-student-task-manager>

3. Open the Spring Boot backend project directory containing `pom.xml` and `mvnw.cmd`.

4. Configure the database connection in `src/main/resources/application.properties` to match your local MySQL settings. Do not commit database passwords, API keys, or other secrets.

5. Start MySQL and ensure that the configured database exists.

6. Start the application on Windows:

   powershell
   .\mvnw.cmd spring-boot:run

7. Open the login page in your browser:

   http://localhost:8080/login.html

The application requires a valid database configuration and the necessary Maven dependencies. Follow the current security configuration when testing authenticated API requests.

## Author

**Ty Mitchell**

Secure Student Task Manager (SSTM) — Software Engineering Project
