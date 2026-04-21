# 🏦 Banking Modern Data Stack

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?logo=snowflake&logoColor=white)
![DBT](https://img.shields.io/badge/dbt-FF694B?logo=dbt&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?logo=apacheairflow&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20?logo=apachekafka&logoColor=white)
![Debezium](https://img.shields.io/badge/Debezium-EF3B2D?logo=apache&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-000000?logo=githubactions&logoColor=white)

---

## 📌 Project Overview
This project demonstrates an **end-to-end modern data stack pipeline** for a **Banking domain**.  
We simulate **customer, account, and transaction data**, stream changes in real time, transform them into analytics-ready models, and visualize insights — following **best practices of CI/CD and data warehousing**.

---

## 🏗️ Architecture  

<img width="5647" height="3107" alt="Architecture" src="https://private-user-images.githubusercontent.com/69398501/581359207-9d968c71-110e-4c99-8129-b8d850112a56.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzY3ODAwODcsIm5iZiI6MTc3Njc3OTc4NywicGF0aCI6Ii82OTM5ODUwMS81ODEzNTkyMDctOWQ5NjhjNzEtMTEwZS00Yzk5LTgxMjktYjhkODUwMTEyYTU2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNjA0MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjYwNDIxVDEzNTYyN1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTk4NDc4NGQ0NzBjZjQ3YWJlNzI1YjgwMmRkYzI3YzJhOWFiOWVjN2QwMWY3NWJhNmIzYTkyMzUxZDJmNjc4MjYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JnJlc3BvbnNlLWNvbnRlbnQtdHlwZT1pbWFnZSUyRnBuZyJ9.EVTq9bbSGYogg4qObK3XHhSBv62TWuGjhphB-KiCKwQ" />


**Pipeline Flow:**
1. **Data Generator** → Simulates banking transactions, accounts & customers (via Faker).  
2. **Kafka + Debezium** → Streams change data (CDC) into MinIO (S3-compatible storage).  
3. **Airflow** → Orchestrates data ingestion & snapshots into Snowflake.  
4. **Snowflake** → Cloud Data Warehouse (Bronze → Silver → Gold).  
5. **DBT** → Applies transformations, builds marts & snapshots (SCD Type-2).  
6. **CI/CD with GitHub Actions** → Automated tests, build & deployment.  

---

## ⚡ Tech Stack
- **Snowflake** → Cloud Data Warehouse  
- **DBT** → Transformations, testing, snapshots (SCD Type-2)  
- **Apache Airflow** → Orchestration & DAG scheduling  
- **Apache Kafka + Debezium** → Real-time streaming & CDC  
- **MinIO** → S3-compatible object storage  
- **Postgres** → Source OLTP system  
- **Python (Faker)** → Data simulation  
- **Docker & docker-compose** → Containerized setup  
- **Git & GitHub Actions** → CI/CD workflows  

---

## ✅ Key Features
- **PostgreSQL OLTP**: Source relational database with ACID guarantees (customers, accounts, transactions)  
- **Simulated banking system**: customers, accounts, and transactions  
- **Change Data Capture (CDC)** via Kafka + Debezium (capturing Postgres WAL)  
- **Raw → Staging → Fact/Dimension** models in DBT  
- **Snapshots for history tracking** (slowly changing dimensions)  
- **Automated pipeline orchestration** using Airflow  
- **CI/CD pipeline** with dbt tests + GitHub Actions  

---

## 📂 Repository Structure
```text
banking-modern-datastack/
├── .github/workflows/         # CI/CD pipelines (ci.yml, cd.yml)
├── banking_dbt/              # DBT project
│   ├── models/
│   │   ├── staging/           # Staging models
│   │   ├── marts/             # Facts & dimensions
│   │   └── sources.yml
│   ├── snapshots/             # SCD2 snapshots
│   └── dbt_project.yml
├── consumer
│   └── kafka_to_minio.py
├── data-generator/            # Faker-based data simulator
│   └── faker_generator.py
├── docker/                    # Airflow DAGs, plugins, etc.
│   ├── dags/                  # DAGs (minio_to_snowflake, scd_snapshots)
├── kafka-debezium/            # Kafka connectors & CDC logic
│   └── generate_and_post_connector.py
├── postgres/                  # Postgres schema (OLTP DDL & seeds)
│   └── schema.sql
├── .gitignore
├── docker-compose.yml         # Containerized infra
├── dockerfile-airflow.dockerfile
├── requirements.txt
└── README.md
```

---

## ⚙️ Step-by-Step Implementation  

### **1. Data Simulation**  
- Generated synthetic banking data (**customers, accounts, transactions**) using **Faker**.  
- Inserted data into **PostgreSQL (OLTP)** so the system behaves like a real transactional database (**ACID, constraints**).  
- Controlled generation via `config.yaml`.  

---

### **2. Kafka + Debezium CDC**  
- Set up **Kafka Connect & Debezium** to capture changes from **Postgres**.  
- Streamed **CDC events** into **MinIO**.  

---

### **3. Airflow Orchestration**  
- Built DAGs to:  
  - Ingest **MinIO data → Snowflake (Bronze)**.  
  - Schedule **snapshots & incremental loads**.  

---

### **4. Snowflake Warehouse**  
- Organized into **Bronze → Silver → Gold layers**.  
- Created **staging schemas** for ingestion.  

---

### **5. DBT Transformations**  
- **Staging models** → cleaned source data.  
- **Dimension & fact models** → built marts.  
- **Snapshots** → tracked history of accounts & customers.  

---

### **6. CI/CD with GitHub Actions**  
- **ci.yml** → Lint, dbt compile, run tests.  
- **cd.yml** → Deploy DAGs & dbt models on merge.  

---

### **7. Data Vizualization**  
The final output of the Gold layer is consumed by a Banking Dashboard to provide actionable business insights:
- **Operational KPIs**: Monitoring total customers, accounts, and transaction volume
- **Transaction Analysis**: Visualizing the proportion of Withdrawals, Transfers, and Deposits to understand liquidity flow.
- **Top Performers**: Identifying high-value customers and accounts based on total transaction amounts. 

<img width="5647" height="3107" alt="Architecture" src="https://private-user-images.githubusercontent.com/69398501/581575276-433f5837-68ad-4b4e-be1a-e1fccc74bf11.jpg?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzY3OTYyNTYsIm5iZiI6MTc3Njc5NTk1NiwicGF0aCI6Ii82OTM5ODUwMS81ODE1NzUyNzYtNDMzZjU4MzctNjhhZC00YjRlLWJlMWEtZTFmY2NjNzRiZjExLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNjA0MjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjYwNDIxVDE4MjU1NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdiZjVhNGRhODdkYzQzZTk5Mzc0MmFiOTNlNDgxMjlkOGVkYjAyZjRhMDQwNzlkZDRkNWE1ZDgxMTllNTc1MTkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JnJlc3BvbnNlLWNvbnRlbnQtdHlwZT1pbWFnZSUyRmpwZWcifQ.VTa7kHWphzRrqP1AEJB2k6UORwzDxaX7lXs3m_HLkNQ" />


---


## 📊 Final Deliverables  
- **Automated CDC pipeline** from Postgres → Snowflake  
- **DBT models** (facts, dimensions, snapshots)  
- **Orchestrated DAGs in Airflow** 
- **Synthetic banking dataset** for demos  
- **CI/CD workflows** ensuring reliability
- **Interactive Banking Dashboard** High-level KPIs, transaction trends, and account rankings

---

**Author**: *Ghany Salam*  
**LinkedIn**: [Ghany Salam](https://www.linkedin.com/in/ghanysalam/)  

