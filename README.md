### Step-by-Step Guide to Deploy a MERN Application Using Docker

This guide walks you through deploying a **MERN (MongoDB, Express, React, Node.js) application** using **Docker**. The setup includes a **MongoDB database**, a **backend API**, and a **React frontend**, all running as Docker containers.

---

### Prerequisites

- **Ubuntu Server** with SSH access.
- **Docker** and **Docker Compose** installed.
- **Basic knowledge of Docker and Linux commands**.

---

### Step 1: Update Your System

Run the following command to update your package list:

```bash
sudo apt update -y
```

---

### Step 2: Install Docker

To install **Docker**, run:

```bash
sudo apt install -y docker.io
```

Give your user permission to access Docker without `sudo`:

```bash
sudo chown $USER /var/run/docker.sock
```

Verify the installation:

```bash
docker --version
```

---

### Step 3: Install Docker Compose

Docker Compose helps manage multi-container applications. Install it using:

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.21.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Make the binary executable:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

Verify the installation:

```bash
docker-compose --version
```

---

### Step 4: Clone the MERN Application Repository

Clone your **MERN application** from GitHub:

```bash
git clone https://github.com/siddhantbhattarai/MERN-Application-Dockerize.git
```

Navigate into the project directory:

```bash
cd MERN-Application-Dockerize/
```

---

### Step 5: Start the Application

Build and start the containers:

```bash
docker-compose up -d --build
```

Verify that the containers are running:

```bash
docker ps
```

You should see three running containers:

- **mern-application-dockerize-frontend** (React app)
- **mern-application-dockerize-backend** (Node.js API)
- **mern-application-dockerize-mongo** (MongoDB database)

---

### Step 6: Connect to the Database

To access MongoDB inside the container:

```bash
docker exec -it mern-application-dockerize-mongo-1 mongosh -u root -p admin --authenticationDatabase admin
```

Once inside MongoDB, list the available databases:

```js
show dbs
```

Switch to the application database (**chatApp** in this case):

```js
use chatApp
```

Show available collections:

```js
show collections
```

If a `users` collection exists, retrieve all users:

```js
db.users.find().pretty()
```

---

### Step 7: Access the Application

- **Frontend (React App):** `http://<your-server-ip>:8080`
- **Backend API:** `http://<your-server-ip>:5001`

Replace `<your-server-ip>` with your actual server IP.

---

### Step 8: Stopping and Cleaning Up

To stop and remove the containers, run:

```bash
docker-compose down
```

This will stop and remove all running containers.

---

### Conclusion

You have successfully deployed a **MERN application** using **Docker**. This guide covered everything from installing Docker and cloning your repository to running your full-stack application in Docker containers.

If you encounter any issues, double-check your **Docker setup** and **container logs** using:

```bash
docker logs <container_id>
```

🚀 Happy Coding!

