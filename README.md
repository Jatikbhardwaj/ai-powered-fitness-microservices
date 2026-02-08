# 🏋️‍♂️🤖 AI-Powered Fitness Microservices

![Java](https://img.shields.io/badge/Java-ED8B00?logo=java&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?logo=springboot&logoColor=white)
![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-6DB33F?logo=spring&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)
![Redux](https://img.shields.io/badge/Redux-764ABC?logo=redux&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?logo=rabbitmq&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Keycloak](https://img.shields.io/badge/Keycloak-BA0000?logo=keycloak&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?logo=google&logoColor=white)
![Eureka](https://img.shields.io/badge/Eureka-FF6F00?logo=java&logoColor=white)

---
## 📘 Overview

**AI-Powered Fitness Microservices** is a robust, scalable, and secure fitness tracking platform built on a
microservices architecture. It empowers users to log physical activities, receive personalized AI-driven workout
recommendations, and manage their profiles with enterprise-grade security.

The backend leverages **Spring Boot** and **Spring Cloud** for modular service development, API Gateway routing, service
discovery, and asynchronous event-driven communication. The frontend is built with **React**, featuring a seamless
OAuth2 PKCE authentication flow powered by **Keycloak**. AI capabilities are integrated using Google's **Gemini API**
for real-time personalized insights.

This system exemplifies modern cloud-native design principles, ensuring resilience, extensibility, and maintainability.

---

## 🏗️ Architecture

![Architecture](/assets/ai-powererd-fitness-microservice-arch.jpg)

---

## 🛠️⚙️️ Technology Stack

### 🧩 Backend

- Java 21, Spring Boot 3
- Spring Cloud Gateway
- Spring WebFlux (Reactive)
- Spring Security (OAuth2 Resource Server)
- Spring Data JPA (PostgreSQL)
- Spring Data MongoDB (Activity & AI Services)
- Netflix Eureka (Service Discovery)
- Spring Cloud Config Server (Centralized Configuration)

### 🎨 Frontend

- React 18+
- Redux Toolkit (State Management)
- Axios (HTTP Client)
- Material UI (UI Components)
- React Router (Routing)
- React OAuth2 Code PKCE (Authentication)

### ☁️ Infrastructure & DevOps

- Keycloak (Identity and Access Management)
- RabbitMQ (Message Broker)
- PostgreSQL (User Service DB)
- MongoDB (Activity & AI Service DBs)
- Docker (Containerization)

### 🤖 AI Integration

- Google Gemini API (Generative AI Model)

---

## 📁🗂️ Project Structure

```text
ai-powered-fitness-microservices/
│
├── gatewayservice/        # API Gateway + Security + User Sync
├── userservice/           # User Management (PostgreSQL)
├── activityservice/       # Activity Tracking (MongoDB)
├── aiservice/             # AI Recommendations (MongoDB + Gemini API)
├── configserver/          # Centralized Configuration Server
├── eureka/                # Service Discovery Server
└── fitness-app-frontend/  # React Frontend Application
```

---

## 🗄️📊 Database Schemas

### 🧑 User Service (PostgreSQL)

- Users table with keycloak user ID mapping and metadata.

### 🏃 Activity Service (MongoDB)

```json
{
  "id": "string",
  "userId": "UUID",
  "type": "RUNNING | WALKING | CYCLING",
  "duration": "number (minutes)",
  "caloriesBurned": "number",
  "startTime": "timestamp",
  "additionalMetrics": {},
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

### 🤖 AI Service (MongoDB)

```json
{
  "id": "string",
  "activityId": "string",
  "userId": "UUID",
  "activityType": "RUNNING | WALKING | CYCLING",
  "recommendation": "string",
  "improvements": {},
  "suggestions": {},
  "safety": {},
  "createdAt": "timestamp"
}
```

---

## 📦🚀 Key Features

- 🔐 Enterprise-grade OAuth2 PKCE authentication with Keycloak.
- 🚪 Centralized API Gateway with route-based request routing and security.
- 👥 Automatic user synchronization with Keycloak identity provider.
- 🏃 Comprehensive activity tracking with flexible metrics.
- 🤖 Real-time AI-powered personalized workout recommendations.
- 📡 Event-driven asynchronous communication via RabbitMQ.
- 🧭 Dynamic service discovery with Eureka.
- ⚙️ Centralized configuration management with Spring Cloud Config.

---

## 🌐🔗 REST API Endpoints

### 🚪Gateway (Single Entry Point)

```
http://localhost:8080
```

### 👤 User Service

| Method | Endpoint                   | Description             |
|--------|----------------------------|-------------------------|
| GET    | `/api/users/{userId}`      | Retrieve user profile   |
| GET    | `/api/users/{id}/validate` | Validate user existence |
| POST   | `/api/users`               | Register new user       |

### 🏃 Activity Service

| Method | Endpoint                       | Description                             |
|--------|--------------------------------|-----------------------------------------|
| GET    | `/api/activities`              | List activities for authenticated user  |
| GET    | `/api/activities/{activityId}` | Get details of a specific activity      |
| POST   | `/api/activities`              | Add new activity for authenticated user |

### 🤖 AI Recommendation Service

| Method | Endpoint                                     | Description                           |
|--------|----------------------------------------------|---------------------------------------|
| GET    | `/api/recommendations/user/{userId}`         | Get AI recommendations for a user     |
| GET    | `/api/recommendations/activity/{activityId}` | Get AI recommendation for an activity |

---

## 🧩📌 Service Responsibilities Summary

| Service          | Responsibilities                                                      |
|------------------|-----------------------------------------------------------------------|
| Gateway          | Authentication, JWT validation, user synchronization, request routing |
| User Service     | User profile management, validation, persistence                      |
| Activity Service | Activity CRUD, event publishing to RabbitMQ                           |
| AI Service       | Consuming activity events, AI recommendation generation and storage   |
| Eureka Server    | Service registration and discovery                                    |
| Config Server    | Centralized configuration management                                  |

---

## 🔐🛡️ Security Architecture

- **Authentication:**  
  Users authenticate via Keycloak using OAuth2 PKCE flow.
- **Authorization:**  
  API Gateway validates JWT tokens issued by Keycloak.
- **Token Flow:**  
  Tokens are passed from client → API Gateway → microservices for access control.
- **User Sync:**  
  User info from JWT token is synchronized with User Service to maintain profile data.

---

## 📈⚡ Scalability & Performance Considerations

- **Caching:** Employ caching strategies at gateway and service layers for frequent queries.
- **Load Balancing:** Client-side via Eureka; gateway routes requests evenly.
- **Horizontal Scaling:** Stateless services enable independent scaling.
- **Asynchronous Messaging:** RabbitMQ decouples services to handle load spikes gracefully.

---

## 📌📝 Assumptions & Constraints

- Stateless microservices except for persistence layers.
- Network latency is within acceptable limits.
- RabbitMQ and Eureka are highly available.
- Keycloak is the trusted identity provider.
- AI API usage fits within free tier limits during development.
- Frontend and backend operate on separate domains requiring CORS policies.

---

## 🏗️📖 Architecture Summary

This AI-Powered Fitness Microservices platform demonstrates a modern, resilient, and secure microservices ecosystem. It
employs asynchronous event-driven communication, centralized authentication and configuration, and integrates AI
services to deliver personalized fitness recommendations. The architecture supports scalability, maintainability, and
extensibility, suitable for enterprise-grade deployments.

---

## 🙌🤝 Contributions & Support

Contributions are welcome! Please open issues or pull requests for improvements, bug fixes, or new features.

---

## 📞📬 Contact

**Author:** Jatik Bhardwaj  
**LinkedIn:** [jatik-bhardwaj](https://www.linkedin.com/in/jatik-bhardwaj-502b30206/)  
**Email:** [jatikbhardwaj@gmail.com](mailto:jatikbhardwaj@gmail.com)

---

## 🌟 Thank You

Thank you for exploring the **AI-Powered Fitness Microservices** application.

I hope this project helps you understand modern **microservices architecture**, **event-driven systems**, and **AI
integration** in real-world applications.

Feedback and contributions are always appreciated!
