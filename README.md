#Smart Budget Tracker

Smart Budget Tracker is a Spring Boot application that helps users manage their expenses, categorize spending, and gain AI-powered financial insights. It also supports Stripe payments for Pro features.

Features

- User registration, login, and profile management
- Expense tracking with category assignment
- Category management (create, update)
- AI-powered monthly financial insights (via Groq API)
- Stripe integration for Pro plan payments
- Admin endpoints for user and expense management
- Session-based authentication

Tech Stack

- Java 17
- Spring Boot 3.x (Web, Data JPA, WebFlux, Security)
- PostgreSQL
- Stripe API
- Groq (OpenAI-compatible) API for AI insights
- Maven

Getting Started

Prerequisites

- Java 17+
- Maven
- PostgreSQL database

Configuration

Edit src/main/resources/application.properties:

Set your PostgreSQL credentials:
  spring.datasource.url=jdbc:postgresql://<host>:<port>/<db>
  spring.datasource.username=<username>
  spring.datasource.password=<password>

Set your Stripe and Groq API keys:
  stripe.api.key=sk_test_...
  stripe.publishable.key=pk_test_...
  groq.api.key=gsk_...

Build & Run

mvn clean install
mvn spring-boot:run

The app runs on http://localhost:8080.

API Endpoints

Public

- POST /public/register — Register a new user

Auth

- POST /auth/login — Login (session-based)
- POST /auth/logout — Logout

User

- GET /users/profile — Get current user profile
- PUT /users/update — Update user profile
- DELETE /users/delete — Delete user account

Categories

- GET /categories/categories — List all categories
- POST /categories/create — Create a category
- PUT /categories/update/{id} — Update a category

Expenses

- POST /expenses/create — Add an expense (fields: description, amount, date, categoryId)
- GET /expenses/my-expenses — List user's expenses
- DELETE /expenses/delete/{id} — Delete an expense

AI Insights

- GET /ai-insights/insight/{month}/{year} — Get AI-generated insight for a month

Payments

- POST /payment/create-checkout-session — Start Stripe payment (plan: monthly/yearly)
- GET /payment/success — Stripe payment success callback
- GET /payment/cancel — Stripe payment cancel callback
- GET /payment/my-payments — List user's payments
- GET /payment/pro-status — Check if user is Pro
- GET /payment/plans — List available plans

Admin

- GET /admin/users — List all users
- GET /admin/getUserById/{id} — Get user by ID
- DELETE /admin/deleteUser/{userId} — Delete user by ID
- GET /admin/expenses — List all expenses
- GET /admin/users/{userId}/expenses — List expenses for a user
- PUT /admin/users/role/{userId}?role=ADMIN — Change user role

Data Model

- User: id, name, email, password, role, isProUser, createdAt
- Category: id, name, description, user
- Expense: id, description, amount, date, user, category
- Payment: id, provider, paymentId, amount, status, createdAt, user

Notes

- Default admin: admin@example.com / admin123
- On registration, default categories are created for each user.
- AI insights require a valid Groq API key.
- Stripe integration is for demonstration; use test keys in development.

License

This project is for educational/demo purposes.
