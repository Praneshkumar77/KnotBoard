# KnotBoard Backend

A simplified Spring Boot backend for a virtual sticky-note board system (college project version).

## Tech Stack
- Spring Boot 3.2.5
- Java 17
- Maven
- Spring Data JPA
- Spring Security + JWT (jjwt)
- MySQL

## Modules
- Authentication: Register, Login (JWT)
- Board Management: Create, View, Update, Delete
- Sticky Notes: Create, View by Board, Update, Delete
- Admin: View Users, Change User Role
- Dashboard: Total Users, Total Boards, Total Notes

## Roles
- ADMIN
- FACILITATOR
- CONTRIBUTOR

New users registering via `/api/auth/register` default to `CONTRIBUTOR`.
Promote a user to `ADMIN` or `FACILITATOR` manually in the database, or via the
`PUT /api/users/{id}/role` endpoint once an ADMIN account exists.

## Setup
1. Create a MySQL database (or let `createDatabaseIfNotExist=true` handle it).
2. Update `src/main/resources/application.properties` with your MySQL username/password.
3. Run:
   ```
   mvn spring-boot:run
   ```
4. API base URL: `http://localhost:8080/api`

## Key Endpoints
| Method | Endpoint | Access |
|---|---|---|
| POST | /api/auth/register | Public |
| POST | /api/auth/admin/register | Public, creates an ADMIN only if no ADMIN exists |
| POST | /api/auth/login | Public |
| POST | /api/auth/admin/login | Public, accepts ADMIN accounts only |
| POST | /api/auth/contributor/login | Public, accepts CONTRIBUTOR accounts only |
| GET/POST | /api/boards | Authenticated |
| PUT/DELETE | /api/boards/{id} | ADMIN, FACILITATOR |
| GET/POST | /api/notes, /api/notes/board/{boardId} | Authenticated |
| PUT/DELETE | /api/notes/{id} | Authenticated |
| GET | /api/users | ADMIN |
| PUT | /api/users/{id}/role | ADMIN |
| GET | /api/dashboard | Authenticated |

## Package Structure
```
com.knotboard
 ├── config         (SecurityConfig)
 ├── controller      (REST controllers)
 ├── dto             (Request/response DTOs)
 ├── entity          (AppUser, Board, StickyNote, Role)
 ├── exception       (ResourceNotFoundException, GlobalExceptionHandler)
 ├── repository      (Spring Data JPA repositories)
 ├── service         (Business logic)
 └── security        (JWT filter, util, user details)
```
