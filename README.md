# DeployX

DeployX is a **developer-first deployment management platform** with a Spring Boot backend and a Next.js frontend. It streamlines the process of deploying, managing, and scaling applications, while integrating infrastructure tools like a PostgreSQL-based ports database for quick reference and allocation.

---

## ✨ Features

* **Multi-Environment Deployments** — Easily manage dev, staging, and production.
* **Ports Database** — PostgreSQL-backed tracking of port usage, preloaded with configurable ranges.
* **Team Roles & Permissions** — RBAC for Admin, Developer, and Viewer roles.
* **Git-Integrated CI/CD** — Deploy directly from GitHub, GitLab, or Bitbucket.
* **Environment Variables Manager** — Securely store and manage secrets.
* **Deployment Logs** — View and search real-time build and deployment logs.
* **Canary & Blue-Green Deployments** *(planned)*.
* **AI Assistance** *(planned)* — Automated error fixes and infra recommendations.

---

## 📋 Prerequisites

* Ubuntu (with sudo access)
* Java 17+
* Node.js 18+
* PostgreSQL
* Maven

---

## ⚙️ Setup Instructions

### 1. Install Dependencies

```bash
sudo apt update
sudo apt install openjdk-17-jdk nodejs npm postgresql postgresql-contrib maven
```

### 2. Setup PostgreSQL Database

Login to PostgreSQL:

```bash
sudo -u postgres psql
```

Create the database and table:

```sql
CREATE DATABASE deployx;
\c deployx;
CREATE TABLE ports (
    port_number INT PRIMARY KEY,
    status VARCHAR(50) NOT NULL
);
```

Insert ports **3001–3099** as `available`:

```sql
DO $$
BEGIN
    FOR i IN 3001..3099 LOOP
        INSERT INTO ports (port_number, status) VALUES (i, 'available');
    END LOOP;
END;
$$;
```

Exit PostgreSQL:

```sql
\q
```

---

### 3. Start Backend (Spring Boot)

```bash
cd backend
mvn spring-boot:run
```

### 4. Start Frontend (Next.js)

```bash
cd frontend
npm install
npm run dev
```

### 5. Access Application

* **Frontend:** [http://localhost:3000](http://localhost:3000)
* **Backend API:** [http://localhost:8080](http://localhost:8080)

---

## 🔒 Security Recommendations

* Create a dedicated `deployx` system user to run services.
* Limit sudo privileges to only necessary commands.
* Store sensitive configs in encrypted vaults.

---

## 🛠 Future Roadmap

* Monitoring & Alerts Dashboard
* Cost Analysis & Optimization Tools
* Plugin Marketplace for custom deployment scripts
* Full Kubernetes & Helm integration

---

With this setup, DeployX comes preloaded with port data from 3001–3099 marked as **available** in PostgreSQL, ready for deployment tracking and automation.
