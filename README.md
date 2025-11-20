# Kim Nguyen Midterm Project - Cloud Computing Fall 2025

## Project Overview
This project demonstrates a multi-container system with:

- **Flask backend** that logs user requests
- **Nginx frontend** serving a static page and reverse proxying API requests
- **Docker Compose** to manage containers, environment variables, mounts, and logs

---

## Project Structure

```bash
kimnguyen_midterm_project/
├── backend/
│ ├── app.py
│ └── Dockerfile
├── frontend/
│ ├── index.html
│ └── nginx.conf
├──logs/
├── docker-compose.yml
└── README.md
```


---

## Prerequisites

- Docker
- Docker Compose
- Linux/macOS/Windows with terminal access

---

## How to Run

1. Clone the repository:

```bash
git clone <your-github-repo-url>
cd kimnguyen_midterm_project
```

2. Build and start the project:

```bash
docker compose up -d
```

3. Verify the frontend:

```bash
curl http://localhost:8090/
```
Expected output:
```bash
<html>
<head><title>Midterm Project</title></head>
<body>
<h1>Hello from Nginx Frontend (kimnguyen)</h1>
</body>
</html>
```

4. Verify the backend logging via frontend proxy:

```bash
curl http://localhost:8090/api/log
```
Expected output:
```bash
Log entry added.
```
Check log file:
```bash
cat logs/kimnguyen_access.log
```
Expected log entries:
```bash
Flask route /log was accessed
Flask route /log was accessed
...
```

5. Optional: Access backend directly:
```bash
curl http://localhost:5000/
```
Expected log entries:
```bash
Updated Flask backend of kimnguyen!
```
6. Rebuilding Backend Only
If you make changes to the backend (app.py):
```bash
cd backend
docker build -t kimnguyen_flask_backend .
```
Restart only the backend container:
```bash
docker compose up -d backend
```
Verify update with curl:
```bash
curl http://localhost:5000/
```

7. Live Log Monitoring

Monitor log file in real time:
```bash
tail -f logs/kimnguyen_access.log
```
Then visit /api/log multiple times to see live updates.

8. Stopping and Cleaning Up
```bash
docker compose down
```
Verify no resources remain:
```bash
docker ps -a
docker images
```

Notes

Backend port: 5000 (internal)

Frontend port: 8090 (external)

Logs are written in logs/kimnguyen_access.log

Environment variable for log path: LOG_PATH=/logs

Author

Kim Nguyen

GitHub: [Your GitHub Link Here]

