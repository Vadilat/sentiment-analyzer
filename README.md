# News Sentiment Analyzer

A Spring Boot microservice that streams live news articles, queues them via Kafka, and performs real-time sentiment analysis using Stanford CoreNLP in a non-blocking WebFlux pipeline.

---

## Tech Stack

- **Java 17**
- **Spring Boot**
- **Spring WebFlux** – Non-blocking reactive web layer
- **Reactor Kafka** – Asynchronous Kafka consumer/producer
- **Stanford CoreNLP** – NLP sentiment analysis
- **NewsAPI** – Fetches live news data
- **Project Reactor** – Flux/Mono reactive programming
- **Maven**

---

## Features

- Streams real-time news articles by keyword
- Performs NLP sentiment analysis using CoreNLP
- Aggregates sentiment scores over time windows
- Kafka-backed message queue (via Reactor Kafka)
- Fully non-blocking REST API with WebFlux
- Endpoints to start/stop news stream on demand

---

## Project Structure
```text
src/
├── controller/ → Exposes all REST endpoints
├── kafka/ → Kafka sender, receiver, topic config
├── news/ → Connects to NewsAPI and emits article lines
├── nlp/ → Stanford CoreNLP sentiment analyzer
└── resources/
└── application.properties
```

---

## API Endpoints

| Method | Endpoint       | Description                                 |
|--------|----------------|---------------------------------------------|
| GET    | `/hello`       | Analyze custom text sentiment               |
| GET    | `/sendKafka`   | Manually send a message to Kafka            |
| GET    | `/getKafka`    | View incoming Kafka messages                |
| GET    | `/startNews`   | Start streaming news by keyword             |
| GET    | `/stopNews`    | Stop the news stream                        |
| GET    | `/grouped`     | View grouped message count by time window   |
| GET    | `/sentiment`   | View average sentiment over time window     |

---

## Running Locally

### Prerequisites:
- Java 17  
- Maven  
- Kafka (locally or via Docker)

---

## Running Locally

### 1. Build & Run the App

```bash
mvn clean install
mvn spring-boot:run
```

### 2. Start Kafka
Make sure Kafka is running locally or via Docker:

#### Using Docker
```bash
docker-compose up -d
```
Ensure that the topic used matches APP_TOPIC defined in KafkaTopicConfig.java

### 3. Configuration
In application.properties:
```bash

spring.kafka.bootstrap-servers=localhost:9092
```
Replace the NewsAPI key in AppNewsStream.java:


```bash
.defaultHeader("X-Api-Key", "your-api-key-here")
```
---

