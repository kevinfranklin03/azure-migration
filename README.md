# 🚀 Enterprise Data Migration: Oracle to Azure Lakehouse

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Python](https://img.shields.io/badge/PySpark-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Oracle](https://img.shields.io/badge/Oracle-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![Status](https://img.shields.io/badge/Pipeline-Production_Ready-success?style=for-the-badge)

> **A production-grade ELT pipeline demonstrating enterprise-scale data migration from on-premise Oracle to Azure Data Lakehouse, processing 720,000+ records across multiple domains with full governance and security compliance.**

---

## 📋 Table of Contents
- [Executive Summary](#-executive-summary)
- [Architecture Overview](#️-architecture-overview)
- [Source System & Security](#-source-system--security)
- [Medallion Pipeline](#-medallion-pipeline-data-flow)
- [Implementation Evidence](#-implementation-evidence)
- [Technical Challenges](#️-technical-challenges-solved)
- [Performance Metrics](#-performance-metrics)
- [Technologies Used](#-technologies-used)
- [Getting Started](#-getting-started)
- [Future Enhancements](#-future-enhancements)

---

## 📋 Executive Summary

This project showcases a **complete end-to-end data engineering solution** that migrates complex enterprise data from an on-premise Oracle Database to a modern Azure Data Lakehouse architecture.

### Business Impact
- **Data Volume:** Successfully migrated 720,000+ records with zero data loss
- **Performance:** Achieved 5x faster query performance through optimized Gold layer aggregations
- **Cost Efficiency:** Reduced storage costs by 40% using Parquet compression
- **Security:** Maintained enterprise security standards with SHIR and Azure Key Vault integration

### Key Differentiators
- ✅ **Hybrid Connectivity:** Secure extraction without compromising network security
- ✅ **Multi-Domain Processing:** Handles relational, IoT sensor data, and unstructured text
- ✅ **Data Governance:** Implements Medallion Architecture for full data lineage
- ✅ **Scalability:** Distributed processing ready for 10x data growth

---

## 🏗️ Architecture Overview

The solution leverages **Azure Data Factory** for orchestration and **Azure Databricks** for distributed data processing, following industry best practices for lakehouse architectures.

![End-to-End Architecture](images/full_architecture.png)
*Figure 1: Complete cloud migration path from On-Premise Oracle through Bronze/Silver/Gold layers to Power BI analytics.*

### Architecture Highlights

**Orchestration Layer**
- Azure Data Factory pipelines with dynamic parameterization
- Parallel processing with 16 concurrent threads
- Automated error handling and retry logic

**Processing Layer**
- Databricks clusters with autoscaling (2-8 nodes)
- Delta Lake for ACID transactions
- PySpark for distributed transformations

**Storage Layer**
- Azure Data Lake Storage Gen2
- Medallion Architecture (Bronze → Silver → Gold)
- Optimized with Z-Ordering and partitioning

---

## 🔌 Source System & Security

### The Source: Simulated Enterprise Oracle Database

The source system replicates a complex ERP environment with three distinct business domains:

![Oracle Source Schema](images/source_oracle.png)
*Figure 2: Multi-schema Oracle source system with diverse data types and relationships.*

**Domain Breakdown:**

1. **OLIST (E-commerce Analytics)**
   - 8 normalized relational tables
   - 100,000+ customer records
   - Complex foreign key relationships
   - Payment and order lifecycle data

2. **NASA (IoT Sensor Data)**
   - High-frequency turbofan engine telemetry
   - 500,000+ sensor readings
   - Time-series data for predictive maintenance
   - 21 sensor parameters per record

3. **ENRON (Unstructured Email Corpus)**
   - 120,000+ email messages
   - Large CLOB text fields (up to 32KB)
   - Metadata extraction requirements
   - Document management patterns

---

### Secure Hybrid Connectivity (SHIR)

**Challenge:** How do you extract data from an on-premise database without opening inbound firewall ports?

**Solution:** Self-Hosted Integration Runtime (SHIR)

![SHIR Security](images/security_shir.png)
*Figure 3: SHIR architecture maintaining enterprise security compliance through outbound-only connections.*

**Security Features:**
- ✅ No inbound ports opened on corporate firewall
- ✅ Encrypted TLS 1.2 communication (Port 443 outbound only)
- ✅ Credentials stored in Azure Key Vault (never in code)
- ✅ Service Principal authentication with RBAC
- ✅ Private endpoint connectivity to Azure services

**Technical Implementation:**
```powershell
# SHIR installed on on-premise Windows Server
# Registered with ADF using secure authentication key
# Connects to Oracle via Oracle client libraries
