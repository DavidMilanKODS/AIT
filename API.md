# AIT - TalentShare: REST API Documentation (Phase 1)

## 1. Authentication Endpoints

### `POST /api/auth/register`
Registers a new user (Buyer or Seller) and creates the corresponding role profile.
- **Request Body**:
```json
{
  "email": "student@ait.edu.bd",
  "password": "Password123!",
  "role": "SELLER",
  "fullName": "Sabbir Hossain"
}
```
- **Response**: `200 OK`
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "uuid",
      "email": "student@ait.edu.bd",
      "role": "SELLER",
      "status": "ACTIVE"
    },
    "token": "jwt_session_token"
  }
}
```

### `POST /api/auth/login`
Authenticates user and sets HTTP-only session cookie `ait_session`.
- **Request Body**:
```json
{
  "email": "student@ait.edu.bd",
  "password": "Password123!"
}
```

### `GET /api/auth/me`
Retrieves current session and profile data.
- **Headers**: `Cookie: ait_session=...` or `Authorization: Bearer <token>`
- **Response**: `200 OK` with user and profile data.

---

## 2. Health & Diagnostics

### `GET /api/health`
System liveness and Phase 1 architecture verification.
- **Response**: `200 OK`
```json
{
  "status": "ok",
  "product": "AIT - TalentShare",
  "phase": "PHASE 1 - FOUNDATION & CORE ARCHITECTURE",
  "timestamp": "2026-09-06T19:54:00.000Z"
}
```

---

## 3. Error Response Standard
All API endpoints follow a consistent error format:
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable description"
  }
}
```
Stack traces and sensitive internals are never exposed in responses.
