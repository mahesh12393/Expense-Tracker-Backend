
# 💸 Expense Tracker – Microservices Architecture

A cloud-native, modular Expense Tracker system built using Java and Spring Boot, designed to handle user authentication, profile management, expense tracking, and real-time SMS parsing using Mistral LLM. The backend follows a distributed microservices architecture, powered by Kafka, Kong API Gateway, and deployed with Docker.

---

## 🧱 Microservices Overview

### 🔐 Auth Service
Handles user **authentication and authorization** using **JWT tokens**.

- **Endpoints**
  - `POST /api/v1/auth/signup` – Register a new user
  - `POST /api/v1/auth/login` – Login and receive JWT
- **Tech**: Java, Spring Boot, MySQL, JWT

---

### 👤 User Service
Manages user **profile data** and validates users during inter-service communication.

- **Endpoints**
  - `GET /api/v1/users` – Get all users
  - `GET /api/v1/users/{id}` – Get user by ID
- **Tech**: Java, Spring Boot, PostgreSQL

---

### 💰 Expense Service
Handles **expense creation, updates, and retrieval**, while publishing events to Kafka.

- **Endpoints**
  - `POST /api/v1/expense` – Create a new expense
  - `GET /api/v1/expense/user/{userId}` – Get user’s expenses
- **Kafka Integration**: Publishes messages for downstream processing
- **Tech**: Java, Spring Boot, PostgreSQL, Apache Kafka

---

### 📊 DS (Data Science) Service
Consumes Kafka messages and uses Mistral LLM to parse SMS content into expenses.

- **Endpoints**
  - `GET /api/v1/ds/message/` – Extracts the entities and push that data to kafka
- **LLM Integration**: Parses unstructured SMS content to structured expenses
- **Tech**: Python, Langchain, Apache Kafka, Mistral LLM API

