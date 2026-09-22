# Digital Document Verification System

A full-stack portfolio project for issuing, storing and verifying digital PDF certificates.

## Stack
- Backend: Java 21, Spring Boot 3.5.6, Spring Web, Spring Data JPA, Hibernate, Spring Security, MySQL
- Frontend: React + Vite + Axios
- Integrity: SHA-256
- Storage: local `uploads/` directory (learning/demo setup)
- Database: MySQL 8

## Features
- Admin-style dashboard
- Issue PDF documents
- Automatic unique certificate IDs (`CERT-YYYY-XXXXXXXX`)
- SHA-256 hash saved at issuance
- Public verification endpoint
- Detects a modified stored PDF as `TAMPERED`
- Revoke a certificate
- Verification history
- PDF viewing/downloading
- React frontend
- MySQL schema managed automatically by JPA
- Docker Compose option for MySQL

## Option A — easiest setup (MySQL installed locally)
1. Install Java 21, Maven 3.9+, Node.js 20+ and MySQL 8+.
2. Start MySQL.
3. Create database:
   ```sql
   CREATE DATABASE document_verification;
   ```
4. Open `src/main/resources/application.properties` and change the password if needed. Default is `root`.
5. Start backend from the project root:
   ```bash
   mvn spring-boot:run
   ```
6. In a second terminal:
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
7. Open the Vite URL shown by the terminal, normally `http://localhost:5173`.

## Option B — Docker MySQL
From the project root:
```bash
docker compose up -d mysql
```
The compose file creates MySQL 8.4 with database `document_verification`, user `root`, password `root`, port `3306`.
Then run the backend and frontend as above.

## Main API endpoints
- `POST /api/documents` — multipart upload: `holderName`, `documentType`, `issuer`, `issueDate`, `file`
- `GET /api/documents` — list documents
- `GET /api/documents/{documentId}` — document details
- `GET /api/documents/{documentId}/file` — PDF
- `PUT /api/documents/{documentId}/revoke` — revoke
- `GET /api/documents/verify/{documentId}` — verify + create log
- `GET /api/documents/stats` — dashboard counters
- `GET /api/documents/logs` — latest verification logs

## Important
This is a learning/portfolio implementation. Authentication is intentionally open in this demo so it runs immediately. For a production deployment, add real JWT authentication and role-based authorization, object storage, malware scanning, rate limiting, HTTPS, secret management and stronger audit controls.
