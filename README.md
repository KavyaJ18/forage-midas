# 🏦 Midas Core — J.P. Morgan Forage Virtual Experience

## 💡 Overview
**Midas Core** is a backend simulation of a financial transaction processing system completed as part of the **J.P. Morgan Software Engineering Virtual Experience Program (Forage)**. It demonstrates how financial institutions process transactions asynchronously, maintain data integrity, and communicate with external services.

The system is built using **Spring Boot**, **Kafka**, **Spring Data JPA**, and an **H2 in-memory database**, and integrates with an external **Incentive REST API** while exposing a REST endpoint for querying user balances.

---

## 🚀 Features
- **Asynchronous Transaction Processing** using Apache Kafka
- **Validation & Persistence** of transactions using H2 + Spring JPA
- **Incentive API Integration** through REST communication
- **REST Endpoint** (`/balance`) for retrieving user account balances
- **Automated Tests** using Embedded Kafka and H2 database

---

## 🧩 System Architecture
```
Frontend → Kafka Topic → Midas Core (Spring Boot)
                           ↓
          ┌──────────Validation──────────┐
          │                              │
Incentive API (via REST)          H2 Database
          │                              │
          └────────────→ /balance REST Endpoint
```

---

## 🧠 How It Works
### 1️⃣ Kafka Listener — Receiving Transactions
- Listens to a Kafka topic defined in configuration.
- Receives and deserializes incoming `Transaction` objects.
- Decouples frontend and backend using asynchronous communication.

### 2️⃣ Validation & Database Recording
A transaction is valid if:
- Sender exists
- Recipient exists
- Sender has enough balance

Valid transactions:
- Stored in the database using JPA
- Deduct amount from sender
- Add amount to recipient

### 3️⃣ Incentive API Integration
- Calls external REST API at `http://localhost:8080/incentive`
- Sends the transaction as JSON
- Receives an incentive amount
- Adds incentive to **recipient's** balance

### 4️⃣ REST API — `/balance`
- Exposes GET endpoint on port **33400**
- Returns a JSON serialized `Balance` object
- Returns `0` if user does not exist

### 5️⃣ Testing
- Includes 5 task-based automated tests
- Uses **embedded Kafka** and **H2 database** for full simulation

---

## 🛠️ Tech Stack
- **Java 17**
- **Spring Boot**
- **Apache Kafka**
- **Spring Data JPA**
- **H2 Database**
- **JUnit 5**
- **RestTemplate** (for external API integration)
- **Maven**

---

## ⚙️ Setup Instructions
### Prerequisites
- Java 17+
- Maven
- Git

### Steps
1. Clone the repo:
   ```bash
   git clone https://github.com/your-username/forage-midas.git
   cd forage-midas
   ```

2. Build the project:
   ```bash
   mvn clean install
   ```

3. Run the Incentive API (from `/services` folder):
   ```bash
   java -jar incentive-api.jar
   ```

4. Run the backend:
   ```bash
   mvn spring-boot:run
   ```

5. Access:
   - **Balance API:** `http://localhost:33400/balance?userId=alice`
   - **H2 Console:** `http://localhost:33400/h2-console`

---

## 🧪 Running Tests
Run all test suites:
```bash
mvn test
```
The test outputs include required result snippets for Forage submissions.

---

## 📊 Sample API Response
```json
{
  "userId": "alice",
  "balance": 1572.5
}
```

---

## 📘 Project Reflection
This project strengthened my understanding of:
- Asynchronous event-driven systems with **Kafka**
- Real-world financial transaction validation
- **JPA entity relationships** and SQL database interactions
- **Microservice communication** using REST APIs
- End-to-end backend architecture suitable for banking systems

It also improved my debugging, testing, and system design reasoning.

---

## 🧑‍💻 Author
**Kavya J**
- Backend Developer (Java | Spring Boot)
- Cloud & AI Integration Enthusiast
- LinkedIn: *your-link*
- Email: *your-email*

---

## 🏅 Issuing Organization
**J.P. Morgan Chase & Co.**  
Software Engineering Virtual Experience Program (Forage)

---

Feel free to explore, clone, or extend this project to dive deeper into backend system design and financial technologies!

