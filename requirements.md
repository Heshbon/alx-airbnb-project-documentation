# Backend Features Specifications

### Overview

This document outlines the technical and functional requirements for core backend features, including API endpoints, input/output specifications, validation rules, and performance criteria.

## 1. User Authentication
  - The authentication system manages user registration, session management and login for both guests and hosts.

### API Endpoints

#### Registration
- **POST /auth/register**
  * Request Body:
    ```json
    {
      "email": "string",
      "password": "string",
      "role": "string",
      "name": "string"
    }
    ```
  * Response:
    ```json
    {
      "token": "string",
      "user": {
        "id": "string",
        "email": "string",
        "role": "string"
      }
    }
    ```

#### Login
- **POST /auth/login**
  * Request Body:
    ```json
    {
      "email": "string",
      "password": "string"
    }
    ```
  * Response:
    ```json
    {
      "token": "string",
      "user": {
        "id": "string",
        "email": "string",
        "role": "string"
      }
    }
    ```

### Validation rules
- Password must be at least 12 characters.
- Email must be valid format.
- Role must be either "guest" or "host".
- All fields are required.

### Performance criteria
- Request capacity: 1000 requests per minute.
- Uptime: 99.9%.
- Response time: < 200ms.

## 2. Property Management

### Overview
The property management system handles property listings, deletions and updates.

### API Endpoints

#### Create property
- **POST /properties**
  * Request Body:
    ```json
    {
      "title": "string",
      "description": "string",
      "price": "number",
      "location": {
        "latitude": "number",
        "longitude": "number"
      },
      "amenities": ["string"]
    }
    ```
  * Response:
    ```json
    {
      "id": "string",
      "hostId": "string",
      "title": "string",
      "description": "string",
      "price": "number",
      "location": {
        "latitude": "number",
        "longitude": "number"
      },
      "amenities": ["string"],
      "createdAt": "timestamp"
    }
    ```

### Validation rules
- Description must be between 20-5000 characters.
- Price must be positive number.
- Title must be between 5-100 characters.
- Location coordinates must be valid.

### Performance criteria
- Request capacity: 500 requests per minute.
- Uptime: 99.5%.
- Response time: < 300ms.

## 3. Booking System

### Overview
The booking system manages property bookings, including updates, creation, and cancellations.

### API Endpoints

#### Create booking
- **POST /bookings**
  * Request Body:
    ```json
    {
      "propertyId": "string",
      "guestId": "string",
      "startDate": "date",
      "endDate": "date",
      "totalCost": "number"
    }
    ```
  * Response:
    ```json
    {
      "id": "string",
      "propertyId": "string",
      "guestId": "string",
      "startDate": "date",
      "endDate": "date",
      "totalCost": "number",
      "status": "string",
      "createdAt": "timestamp"
    }
    ```

### Validation rules
- Property must be available for the dates.
- Dates must be valid and future-dated.
- Guest must be registered user.
- Total cost must be positive.

### Performance criteria
- Request capacity: 200 requests per minute.
- Response time: < 400ms.
- Uptime: 99%.
