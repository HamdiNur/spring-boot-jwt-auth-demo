# Spring Boot JWT Auth Demo

A small, self-contained User Auth API built with **Spring Boot 4** + **Spring Security** + **JWT**, backed by **PostgreSQL running in Docker**. Built as a learning project to practice stateless authentication.

## Features

- User registration with BCrypt password hashing
- Login with JWT issuance
- Stateless authentication (no server-side sessions)
- Protected route example (`/me`) that requires a valid token

## Tech Stack

- Java 21
- Spring Boot 4.1.0
- Spring Security 7
- PostgreSQL 16 (Docker)
- JJWT (`io.jsonwebtoken`) for token generation/validation

## Running Locally

1. Start the database:
   ```bash
   docker compose up -d postgres
   ```
2. Run the app (via IDE or):
   ```bash
   ./mvnw spring-boot:run
   ```
3. The API runs on `http://localhost:8080`

## Endpoints

| Method | Endpoint         | Auth required | Description              |
|--------|------------------|----------------|---------------------------|
| POST   | `/auth/register` | No             | Create a new user         |
| POST   | `/auth/login`    | No             | Log in, returns a JWT     |
| GET    | `/me`            | Yes (Bearer)   | Returns the current user  |

### Example: Register
```json
POST /auth/register
{
  "username": "testuser",
  "password": "testpass123"
}
```

### Example: Login
```json
POST /auth/login
{
  "username": "testuser",
  "password": "testpass123"
}
```
Returns:
```json
{
  "token": "eyJhbGciOi...",
  "tokenType": "Bearer"
}
```

Use the returned token as `Authorization: Bearer <token>` on protected routes.

## Notes

This is a learning/demo project. The JWT secret and database credentials in `application.properties` are placeholder test values — replace them before using this as a base for anything real.