# DevPlaza - Running Locally with Docker Compose

This guide explains how to run the DevPlaza microservices locally using Docker Compose and how to connect your own PostgreSQL database.

## Prerequisites
Before proceeding, ensure you have the following installed:
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- A PostgreSQL database (local or cloud-based)

## Setting Up the Environment
### 1. Configure Database Connection
DevPlaza services require a PostgreSQL database. Set the required database credentials as environment variables:
sh
export DB_USER=<your_db_user>
export DB_PASSWORD=<your_db_password>
export DB_HOST=<your_db_host>
export DB_PORT=<your_db_port>

- Replace <your_db_user> with your PostgreSQL username.
- Replace <your_db_password> with your PostgreSQL password.
- Replace <your_db_host> with your PostgreSQL host (e.g., localhost for a local database, or a remote URL).
- Replace <your_db_port> with your PostgreSQL port (default is 5432).

### 2. Running Docker Compose
Once the environment variables are set, start the services with:
sh
docker-compose up -d

This will pull the latest images from Docker Hub and start all services in detached mode.

### 3. Verifying Running Services
To check running containers, use:
sh
docker ps

Each microservice should be running on its respective port:
- Auth Management: 3000
- Tenant Management: 3001
- User Management: 3002
- Product Management: 3004
- Frontend: 5173

### 4. Stopping Services
To stop the running services, use:
sh
docker-compose down


### 5. Logs & Debugging
To view logs of a specific service:
sh
docker logs -f <container_name>

Example:
sh
docker logs -f auth-mgmt


### 6. Connecting to the Database
To manually connect to your PostgreSQL database, use the following command:
sh
psql -h $DB_HOST -U $DB_USER -d postgres -p $DB_PORT

If using a local PostgreSQL instance, you may need to ensure it is running:
sh
sudo systemctl start postgresql


## Notes
- Ensure your database allows connections from Docker containers.
- If using a cloud-hosted database, whitelist your IP to allow connections.
- If changes are made to the environment variables, restart Docker Compose using:
  sh
  docker-compose down && docker-compose up -d
  

---
Now, your DevPlaza services are running locally and connected to your database! 🚀