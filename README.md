# Cloud-Sandbox
# Cloud-Native Sandbox: Multi-Tier Architecture

## Overview
This project provides a containerized, 3-tier sandbox environment designed to simulate production-grade cloud service orchestration. The architecture emphasizes **service decoupling**, **network isolation**, and **resiliency**.

## Architecture Diagram


## Design Decisions

### 1. Service Decoupling
By containerizing the web server (Nginx) and the database (PostgreSQL), I have decoupled the application layer from the data persistence layer. This is a core tenant of cloud-native development, allowing each service to be updated, scaled, and managed independently.

### 2. Network Segmentation
I implemented custom Docker networks (`frontend` and `backend`) to enforce network isolation. 
- The `web` service exists in the `frontend` network.
- The `db` service exists in the `backend` network.
- **Security Impact:** This follows the **Principle of Least Privilege**, ensuring that only authorized traffic can interact with the database, mimicking a hardened cloud security posture.

### 3. Resiliency Policies
Each container utilizes `restart: always` policies. In a production cloud environment, this ensures the system is self-healing, minimizing downtime by automatically recovering services if they crash.

## Security Considerations
In a production deployment, this architecture would be further hardened by:
- **Secret Management:** Moving the database password from the `docker-compose` file to a secure Secret Manager (e.g., HashiCorp Vault or AWS Secrets Manager).
- **Environment Parity:** Ensuring variables are injected via environment files (`.env`) to separate configuration from infrastructure code.
- **Monitoring:** Integrating centralized logging (like ELK stack or Wazuh) to monitor the traffic between these tiers for anomalous activity.

---
