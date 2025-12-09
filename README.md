### Repository Structure

kafka-elk-monitoring/
├── docker-compose.yml         # All-in-one Docker Compose for Kafka + ELK
├── logstash/
│   └── pipeline.conf          # Logstash pipeline to parse Kafka logs
├── elasticsearch/
│   └── elasticsearch.yml      # Optional ES config for production
├── kibana/
│   └── dashboards/            # Exported NDJSON dashboards (if any)
├── README.md                  # Project overview, setup instructions
└── .gitignore


# Kafka ELK Monitoring

Production-ready Kafka logging and monitoring stack using **Docker Compose**.

## Overview

This repository provides a complete setup for:

- Kafka in **KRaft mode** (single broker)  
- ELK stack (Elasticsearch + Logstash + Kibana) for **centralized logs**  
- Real-time Kafka log visualization in **Kibana dashboards**  
- Optional monitoring via **Prometheus/Grafana** (metrics)  

Ideal for **high-security, high-scalable environments** like banking.

---

## Prerequisites

- Docker >= 24.x  
- Docker Compose >= 2.x  
- Java 17+ (for Kafka if running locally)  

---

## Setup

1. Clone the repository:

```bash
git clone https://github.com/manikandanramasamy/kafka-elk-monitoring.git
cd kafka-elk-monitoring
```
2. Start all services:

```bash
docker-compose up -d
```

3 .Verify services:

Kafka: localhost:9092

Kibana: http://localhost:5601

Elasticsearch: http://localhost:9200

Logstash: logs automatically sent to Elasticsearch


Logstash Pipeline

Example pipeline in logstash/pipeline.conf:
```yaml
input {
  file {
    path => "/var/log/kafka/*.log"### Repository Structure

kafka-elk-monitoring/
├── docker-compose.yml         # All-in-one Docker Compose for Kafka + ELK
├── logstash/
│   └── pipeline.conf          # Logstash pipeline to parse Kafka logs
├── elasticsearch/
│   └── elasticsearch.yml      # Optional ES config for production
├── kibana/
│   └── dashboards/            # Exported NDJSON dashboards (if any)
├── README.md                  # Project overview, setup instructions
└── .gitignore


# Kafka ELK Monitoring

Production-ready Kafka logging and monitoring stack using **Docker Compose**.

## Overview

This repository provides a complete setup for:

- Kafka in **KRaft mode** (single broker)  
- ELK stack (Elasticsearch + Logstash + Kibana) for **centralized logs**  
- Real-time Kafka log visualization in **Kibana dashboards**  
- Optional monitoring via **Prometheus/Grafana** (metrics)  

Ideal for **high-security, high-scalable environments** like banking.

---

## Prerequisites

- Docker >= 24.x  
- Docker Compose >= 2.x  
- Java 17+ (for Kafka if running locally)  

---

## Setup

1. Clone the repository:

```bash
git clone https://github.com/manikandanramasamy/kafka-elk-monitoring.git
cd kafka-elk-monitoring
```
2. Start all services:

```bash
docker-compose up -d
```

3 .Verify services:

Kafka: localhost:9092

Kibana: http://localhost:5601

Elasticsearch: http://localhost:9200

Logstash: logs automatically sent to Elasticsearch


Logstash Pipeline

Example pipeline in logstash/pipeline.conf:
```yaml
input {
  file {
    path => "/var/log/kafka/*.log"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{TIMESTAMP_IS### Repository Structure

kafka-elk-monitoring/
├── docker-compose.yml         # All-in-one Docker Compose for Kafka + ELK
├── logstash/
│   └── pipeline.conf          # Logstash pipeline to parse Kafka logs
├── elasticsearch/
│   └── elasticsearch.yml      # Optional ES config for production
├── kibana/
│   └── dashboards/            # Exported NDJSON dashboards (if any)
├── README.md                  # Project overview, setup instructions
└── .gitignore


# Kafka ELK Monitoring

Production-ready Kafka logging and monitoring stack using **Docker Compose**.

## Overview

This repository provides a complete setup for:

- Kafka in **KRaft mode** (single broker)  
- ELK stack (Elasticsearch + Logstash + Kibana) for **centralized logs**  
- Real-time Kafka log visualization in **Kibana dashboards**  
- Optional monitoring via **Prometheus/Grafana** (metrics)  

Ideal for **high-security, high-scalable environments** like banking.

---

## Prerequisites

- Docker >= 24.x  
- Docker Compose >= 2.x  
- Java 17+ (for Kafka if running locally)  

---

## Setup

1. Clone the repository:

```bash
git clone https://github.com/manikandanramasamy/kafka-elk-monitoring.git
cd kafka-elk-monitoring
```
2. Start all services:

```bash
docker-compose up -d
```

3 .Verify services:

Kafka: localhost:9092

Kibana: http://localhost:5601

Elasticsearch: http://localhost:9200

Logstash: logs automatically sent to Elasticsearch


Logstash Pipeline

Example pipeline in logstash/pipeline.conf:
```yaml
input {
  file {
    path => "/var/log/kafka/*.log"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{TIMESTAMP_ISO8601:timestamp} %{LOGLEVEL:level} %{GREEDYDATA:msg}" }
  }
  date {
    match => [ "timestamp", "ISO8601" ]
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "kafka-logs-%{+YYYY.MM.dd}"
  }
  stdout { codec => rubydebug }
}

``` 
## Notes

For production, enable persistent volumes for Kafka, Elasticsearch, and Logstash

Consider security configs: TLS, authentication, RBAC for Elasticsearch/Kibana

