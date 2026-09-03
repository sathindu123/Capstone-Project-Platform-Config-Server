# ⚙️ Config-Server

Centralized external configuration server for the ECA microservices ecosystem. It serves configuration properties to all registered services from a single source, enabling environment-specific settings without redeployment.

## 📌 Student & Project Information

| Field | Details |
|---|---|
| **Student Name** | Sathindu Sathsara Kumara |
| **Student Number** | 241711053 |
| **GCP Project ID** | sathindu-gcp-lab |
| **Submission Type** | Alternative Option (Capstone Project) |

## 📖 About

This project is part of the Enterprise Cloud Application (ECA) module in the Higher Diploma in Software Engineering (HDSE) program at the Institute of Software Engineering (IJSE). It is intended exclusively for students enrolled in this program.

Config-Server is the single source of truth for configuration across the entire ECA microservices platform. Every other service — Service-Registry, Api-Gateway, Student-Service, Program-Service, and Enrollment-Service — bootstraps by fetching its configuration from this server before starting up, decoupling configuration entirely from application code.

## 🛠️ Tech Stack

| Technology | Details |
|---|---|
| **Java** | 25 |
| **Spring Boot** | 4.1.0 |
| **Spring Cloud** | 2025.1.2 |
| **Spring Cloud Config Server** | Native filesystem backend |
| **Spring Boot Actuator** | Health & management endpoints |

## 🔍 How It Works

The Config-Server uses a native filesystem backend, loading configuration files from the classpath. All microservices bootstrap by importing their configuration from this server before starting up.

## 📁 Configuration Layout

```text
src/main/resources/configurations/
├── application.yaml          # Shared config for all services (Eureka URL, logging)
├── platform/
│   ├── api-gateway.yaml      # Api-Gateway routes & CORS config
│   └── service-registry.yaml # Eureka server settings
└── services/
    ├── student-service.yaml     # Student-Service datasource (PostgreSQL)
    ├── program-service.yaml     # Program-Service datasource (MongoDB)
    └── enrollment-service.yaml  # Enrollment-Service datasource (MySQL)
```

## ⚙️ Service Details

| Property | Value |
|---|---|
| **Port** | 9000 |
| **Artifact ID** | Config-Server |
| **Group ID** | lk.ijse.eca |

## 🏛️ How This Service Fits the Architecture

```text
┌─────────────────────────────┐
│     Config-Server (9000)    │
│  • application.yaml         │
│  • platform/*.yaml          │
│  • services/*.yaml          │
└──────────────┬──────────────┘
               │ served on startup
   ┌───────────┼────────────┬──────────────┬────────────────┐
   ▼           ▼            ▼              ▼                ▼
Service-   Api-Gateway   Student-      Program-       Enrollment-
Registry   (7000)        Service       Service        Service
(9001)                   (8000)        (8001)         (8002)
```

## 🚀 Getting Started

Follow the lecture guidelines, refer to the lecture video for more information and how to get started correctly.

⚠️ **Important:** Config-Server must be started **first** before any other service, as all other services fetch their configuration from this server on startup.

### ▶️ Run the Service

```bash
./mvnw spring-boot:run
```
The server will be available at: `http://localhost:9000`

## ✅ Verify Configuration Delivery

You can verify a service's configuration is being served correctly by visiting:

```text
http://localhost:9000/{service-name}/default
```

## 💬 Need Help?

If you encounter any issues, feel free to reach out and start a discussion via the Slack workspace.

## 📄 License

This project was developed as part of the Enterprise Cloud Architecture university module (Capstone Project — Alternative Option).
