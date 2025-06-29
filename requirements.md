**Detailed specifications** for three core backend features: **User Authentication**, **Property Management**, and **Booking System**.

---

## 📄 `requirements.md` (place in the root of your repo)

````markdown
# 📌 Airbnb Clone – Backend Feature Requirements

This document outlines the functional and technical specifications for key backend features of the Airbnb Clone project.

---

## 1️⃣ User Authentication

### 🔧 Feature Overview
Handles user sign-up, login, and secure session management using JWT.

### 🛠️ API Endpoints

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/profile` (protected)

### 📥 Input Specifications

#### Registration
```json
{
  "first_name": "Nonie",
  "last_name": "Masuku",
  "email": "nonie@example.com",
  "password": "SecurePass123",
  "role": "guest"
}
````

#### Login

```json
{
  "email": "nonie@example.com",
  "password": "SecurePass123"
}
```

### 📤 Output

* On success:

```json
{
  "token": "jwt_token_here",
  "user": {
    "id": "uuid",
    "first_name": "Nonie",
    "email": "nonie@example.com",
    "role": "guest"
  }
}
```

* On error:

```json
{
  "error": "Invalid credentials"
}
```

### ✅ Validation Rules

* Email must be unique and valid.
* Password: minimum 8 characters, alphanumeric.
* Role must be one of: `guest`, `host`.

### 🚀 Performance Criteria

* Response time < 500ms.
* JWT token expiry: 24 hours.
* Rate limiting: max 10 login attempts per hour.


## 2️⃣ Property Management

### 🔧 Feature Overview

Allows hosts to create, update, and delete listings.

### 🛠️ API Endpoints

* `POST /api/properties` (host only)
* `PUT /api/properties/:id`
* `DELETE /api/properties/:id`
* `GET /api/properties`
* `GET /api/properties/:id`

### 📥 Input Specifications

```json
{
  "name": "Ocean View Apartment",
  "description": "Beautiful sea-facing property.",
  "location": "Cape Town, SA",
  "pricepernight": 120.00
}
```

### 📤 Output

* On creation:

```json
{
  "message": "Property listed successfully",
  "property_id": "uuid"
}
```

### ✅ Validation Rules

* Name, description, location are required.
* Price must be a positive decimal.
* Only users with role `host` can list properties.

### 🚀 Performance Criteria

* Fetch properties with optional filters (location, price).
* Pagination for large datasets (default: 10 per page).
* CRUD operations must complete in < 800ms.


## 3️⃣ Booking System

### 🔧 Feature Overview

Enables guests to book available properties and track booking status.

### 🛠️ API Endpoints

* `POST /api/bookings`
* `GET /api/bookings/:id`
* `GET /api/bookings?user_id=...`
* `PATCH /api/bookings/:id/cancel`

### 📥 Input Specifications

```json
{
  "property_id": "uuid",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05"
}
```

### 📤 Output

* On success:

```json
{
  "message": "Booking successful",
  "booking_id": "uuid",
  "total_price": 480.00,
  "status": "confirmed"
}
```

* On error:

```json
{
  "error": "Property is not available for selected dates"
}
```

### ✅ Validation Rules

* Dates must be in the future.
* No overlapping bookings for the same property.
* Total price = nights × price per night.

### 🚀 Performance Criteria

* Prevent race conditions with atomic checks on booking.
* Booking creation < 1 second.
* Support cancellation policy enforcement.

## 📌 Notes

* All endpoints follow RESTful standards.
* All protected routes require JWT-based authentication.
* Admin users have full access to manage users, properties, and bookings.


## ✅ Next Steps

1. Save this content as `requirements.md` in the **root** of your repo.
2. Then commit and push:

```bash
git add requirements.md
git commit -m "Add detailed requirements for user auth, properties, and booking features"
git push origin main
````



