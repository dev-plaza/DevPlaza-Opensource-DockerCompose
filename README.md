# DevPlaza - Run Locally with Docker Compose

This guide explains how to run **DevPlaza microservices** locally using **Docker Compose** and connect them to a **PostgreSQL database**.

---

## Prerequisites

Before you start, make sure you have:

✅ [Docker](https://www.docker.com/get-started) installed  
✅ [Docker Compose](https://docs.docker.com/compose/install/) installed  
✅ A **PostgreSQL database** (either local or cloud-based)  

---

## Step 1: Configure the Database

DevPlaza requires a **PostgreSQL database** to store data.

### Update `.env` File

Open the `.env` file and update the database details:

```env
DB_USER=your_db_user        # Replace with your PostgreSQL username  
DB_PASSWORD=your_db_password # Replace with your PostgreSQL password  
DB_HOST=your_db_host        # Replace with your PostgreSQL host (e.g., `localhost` or a remote URL)  
DB_PORT=5432                # Replace with your PostgreSQL port (default: 5432)  
```

---

## Step 2: Start the Services

Once the `.env` file is updated, run the following command to start all services:

```sh
docker-compose up -d
```

🔹 This command will start all microservices in **detached mode** (running in the background).

---

## Step 3: Check Running Services

To verify if the services are running, use:

```sh
docker ps
```

Each microservice should be running on its assigned port:

- **Auth Management** → `3000`  
- **Tenant Management** → `3001`  
- **User Management** → `3002`  
- **Product Management** → `3004`  
- **Frontend** → `5173`  

---

## Step 4: Stop Services

To stop all running services, use:

```sh
docker-compose down
```

---

## Step 5: View Logs & Debugging

To check logs of any specific service, run:

```sh
docker logs -f <container_name>
```

For example, to check logs for **Auth Management**, use:

```sh
docker logs -f auth-mgmt
```

---

## Step 6: Connect to the Database

To manually connect to the PostgreSQL database, use:

```sh
psql -h $DB_HOST -U $DB_USER -d postgres -p $DB_PORT
```

If you are using a **local PostgreSQL instance**, ensure it is running:

```sh
sudo systemctl start postgresql
```

---

## Important Notes

- Ensure your **PostgreSQL database** allows connections from Docker containers.  
- If using a **cloud database**, whitelist your **IP address** for access.  
- If you change the `.env` file, restart the services:

```sh
docker-compose down && docker-compose up -d
```

---

## You're All Set! 🚀

Now your **DevPlaza services** are running locally and connected to your database! 🎉

