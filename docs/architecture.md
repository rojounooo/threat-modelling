# Architecture – To-Do List Web App

## Overview
This web application allows users to register, log in, and manage personal to-do notes. The system consists of a frontend web UI, a backend API, and a database for storing user credentials and notes.

## Components
- **Frontend:** Web UI built with HTML/CSS/JS
- **Backend API:** Handles authentication, session management, and CRUD operations for notes
- **Database:** Stores user data and notes (hashed passwords)

## Data Flow
1. User enters credentials in login form
2. Credentials sent over HTTPS to backend
3. Backend verifies credentials against database
4. If valid, backend issues a session token (JWT/cookie)
5. User uses token for subsequent API requests
6. User can create, update, delete notes via API

## Trust Boundaries
- **User device ↔ Server:** Internet boundary, data can be intercepted if HTTPS is not enforced
- **Server ↔ Database:** Internal boundary; database credentials must be protected

## Diagram (simplified)

[User] <--> HTTPS <--> [Backend API] <--> [Database]

## Technology Stack (Hypothetical)

- Frontend: React 
- Backend: Node.js 
- Database: PostgreSQL 