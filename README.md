# 🛒 RoboShop Microservices Application (Docker Compose)

This project sets up the **RoboShop microservices application** using Docker Compose. It includes multiple services like frontend, catalogue, user, cart, shipping, payment, and supporting databases/message brokers.

---

## 📦 Architecture Overview

The application follows a microservices architecture with the following components:

### 🧩 Services

* **Frontend** – User interface (Nginx)
* **Catalogue** – Product catalog service
* **User** – User management service
* **Cart** – Shopping cart service
* **Shipping** – Shipping service
* **Payment** – Payment processing service

### 🗄️ Databases & Messaging

* **MongoDB** – Used by Catalogue & User services
* **MySQL** – Used by Shipping service
* **Redis** – Used by User & Cart services (caching)
* **RabbitMQ** – Used by Payment service (message broker)

---

## 🐳 Docker Compose Setup

This project uses Docker Compose with:

* Custom bridge network (`roboshop`)
* Named volumes for persistent storage
* Service dependencies via `depends_on`

---

## 📁 Project Structure

```
.
├── catalogue/
├── user/
├── cart/
├── shipping/
├── payment/
├── frontend/
├── mongodb/
├── mysql/
├── docker-compose.yml
└── README.md
```

Each service directory contains its own `Dockerfile`.

---

## ⚙️ Prerequisites

Make sure you have installed:

* Docker
* Docker Compose

Verify installation:

```bash
docker --version
docker compose version
```

---

## 🚀 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/roboshop.git
cd roboshop
```

### 2. Start All Services

```bash
docker compose up -d
```

### 3. Check Running Containers

```bash
docker ps
```

---

## 🌐 Access the Application

* Frontend will be available at:

```
http://localhost
```

---

## 🔄 Service Dependencies

| Service   | Depends On                               |
| --------- | ---------------------------------------- |
| catalogue | mongodb                                  |
| user      | redis, mongodb                           |
| cart      | redis, catalogue                         |
| shipping  | cart, mysql                              |
| payment   | rabbitmq, user, cart                     |
| frontend  | catalogue, user, cart, shipping, payment |

---

## 💾 Volumes

Persistent volumes are used for:

* `mongodb` → `/data/db`
* `redis` → `/data`
* `mysql` → `/var/lib/mysql`
* `rabbitmq` → `/var/lib/rabbitmq`

---

## 🔐 Default Credentials

### RabbitMQ

* **Username:** `roboshop`
* **Password:** `roboshop123`

---

## 🛠️ Useful Commands

### Stop Services

```bash
docker compose down
```

### Rebuild Services

```bash
docker compose up -d --build
```

### View Logs

```bash
docker compose logs -f
```
