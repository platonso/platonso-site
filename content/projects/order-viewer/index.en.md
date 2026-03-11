---
title: "Order viewer"
date: 2025-11-10
description: "Service for receiving and viewing marketplace orders"
tags: ["go", "backend"]

---

[![GitHub - order-viewer](https://img.shields.io/badge/GitHub-order--viewer-blue?logo=github&logoColor=white)](https://github.com/platonso/order-viewer)

---

 <img src="/projects/order-viewer/images/screen.png" alt="screen" style="display: block; margin: 0 auto; max-width: 100%;">


### About the Project

The service is designed to receive, process, and store order data coming through Kafka. The main goal is to ensure reliable storage of orders in PostgreSQL and fast access through in-memory caching. The service includes a simple web interface for viewing order information by its identifier.

### Key Features

**Kafka Integration.** The service subscribes to a topic with order data and processes incoming messages in real-time.

**Validation & Error Handling.** Invalid or malformed messages are logged and ignored without disrupting the service.

**PostgreSQL Storage.** Order data is saved to a normalized database structure using transactions to ensure data integrity.

**In-memory Caching.** Recent orders are stored in memory (map) for instant access without database queries.

**Cache Recovery on Startup.** On startup, the service automatically populates the cache with data from the database, ensuring fault tolerance after restarts.

**HTTP API.** Endpoint for retrieving order data by ID (JSON) with priority access to cache and fallback to the database.

**Web Interface.** Simple HTML page for entering an order ID and displaying information received from the API.

### Architectural Decisions

The service is built with Go, ensuring high performance when handling large message streams. A reliable Kafka client with message acknowledgment (commit) is used to guarantee that data is not lost during failures.

The PostgreSQL database is designed according to the incoming JSON structure: orders are stored in related tables (order, delivery, payment, items) for data normalization.

The cache is implemented as a thread-safe structure with mutexes, allowing safe concurrent access from multiple goroutines.

### Error Handling & Fault Tolerance

- Database transactions guarantee atomicity when saving related data
- Kafka messages are acknowledged only after successful storage in the database
- All errors are logged for monitoring and debugging

### Tech Stack

- **Language:** Go 1.22+
- **Message Broker:** Apache Kafka
- **Database:** PostgreSQL
- **Caching:** In-memory
- **Containerization:** Docker, Docker Compose