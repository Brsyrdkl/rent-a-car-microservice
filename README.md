
# 🚗 Rent‑A‑Car Microservices Architecture

This project is a microservices-based car rental system built with Spring Boot and Spring Cloud. It demonstrates key architectural patterns like service discovery, centralized configuration, distributed tracing, API gateway routing, asynchronous messaging, observability, and Docker-based orchestration.

---

## 📁 Project Structure

```
rent-a-car-microservice/
├── api-gateway
├── config-server
├── discovery-server
├── filter-service
├── inventory-service
├── invoice-service
├── maintenance-service
├── payment-service
├── rental-service
├── docker-compose.yml
├── prometheus.yml
├── grafana_json_model.json
└── .gitignore
```

> 🔧 Central configuration files are stored in a separate Git repository:  
> 👉 [config-server-rent-a-car](https://github.com/Brsyrdkl/config-server-rent-a-car)

---

## 🛠️ Tech Stack

- **Java 17** with **Spring Boot**
- **Spring Cloud** (Eureka, Config Server, Gateway, Sleuth, OpenFeign)
- **Kafka** for asynchronous messaging
- **MongoDB** for inventory
- **PostgreSQL** for rentals, payments, maintenance, and invoicing
- **Prometheus & Grafana** for metrics and monitoring
- **Zipkin** for distributed tracing
- **Docker & Docker Compose** for containerization and orchestration

---

## 🚀 Getting Started

### 🧰 Prerequisites

- Java 17+
- Maven
- Docker & Docker Compose

### ▶️ Run the System

```bash
git clone https://github.com/Brsyrdkl/rent-a-car-microservice.git
git clone https://github.com/Brsyrdkl/config-server-rent-a-car.git
cd rent-a-car-microservice
docker-compose up --build
```

This will start:

- Config Server
- Eureka Discovery Server
- API Gateway
- All core microservices
- Kafka + Zookeeper
- MongoDB + PostgreSQL
- Zipkin + Prometheus + Grafana

---

## ⚙️ Configuration Management

All configuration files are hosted in the external repo:  
👉 [`config-server-rent-a-car`](https://github.com/Brsyrdkl/config-server-rent-a-car)

Each service has:
```
service-name-dev.yml
service-name-prod.yml
```

> Services load their configuration from the config server at runtime based on the `SPRING_PROFILES_ACTIVE` environment variable.

To change profiles:
```yaml
environment:
  - SPRING_PROFILES_ACTIVE=dev
```

---

## 🔍 Observability & Monitoring

| Tool       | Purpose                       | URL                  |
|------------|-------------------------------|----------------------|
| Eureka     | Service discovery dashboard   | `http://localhost:8761` |
| Zipkin     | Distributed tracing           | `http://localhost:9411` |
| Prometheus | Metrics scraping              | `http://localhost:9090` |
| Grafana    | Dashboard visualization       | `http://localhost:3000` |

📊 The Grafana dashboard can be imported using the included `grafana_json_model.json`.

---

## 💬 Messaging with Kafka

- `rental-service` emits events to Kafka topics.
- Future services (e.g., `notification-service`) can consume those events for asynchronous processing.
- Kafka and Zookeeper are started automatically with Docker.

---

## 📡 Microservices Summary

| Service             | Port  | DB        | Description                          |
|---------------------|-------|-----------|--------------------------------------|
| config-server        | 8888  | —         | Loads config from Git repo           |
| discovery-server     | 8761  | —         | Eureka registry                      |
| api-gateway          | 8080  | —         | Routes and filters incoming requests |
| rental-service       | ----  | PostgreSQL| Handles rental transactions          |
| inventory-service    | ----  | MongoDB   | Manages vehicle inventory            |
| maintenance-service  | ----  | PostgreSQL| Manages maintenance operations       |
| payment-service      | ----  | PostgreSQL| Processes payments                   |
| invoice-service      | ----  | PostgreSQL| Generates invoices                   |
| filter-service       | ----  | PostgreSQL| Filtering/search across inventory    |

---

## 🧪 Testing

- REST endpoints can be tested with tools like Postman, Swagger or Insomnia.
- Spring Boot Actuator endpoints are exposed for monitoring and health checks.
- Example endpoints:
  - `GET /inventory-service/api/cars`
  - `POST /payment-service/api/payments`
  - `GET /invoice-service/api/invoices/{id}`

---

## 🔐 Security

Security is in this version :
- Spring Security
- OAuth2 or JWT authentication (Keycloak)
- Role-based access at the API Gateway level

---

## 🚧 Roadmap

- [ ] Implement centralized logging (e.g., ELK stack)
- [ ] Add `notification-service` consuming Kafka messages
- [ ] OAuth2/JWT integration for secure APIs
- [ ] Add resilience with Resilience4j
- [ ] CI/CD pipeline and test coverage reporting

---

## 👨‍💻 Author

**Barış Yurdakul**  
Computer Engineering Student @ Gebze Technical University  
🔗 [GitHub Profile](https://github.com/Brsyrdkl)

---
