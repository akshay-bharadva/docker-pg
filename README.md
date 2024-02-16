# docker-pg

[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-12-blue.svg)](https://www.postgresql.org/) [![Docker](https://img.shields.io/badge/Docker-20.10+-blue.svg)](https://www.docker.com/) [![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)

A straightforward and reusable Docker setup for running a PostgreSQL 12 database. This project simplifies the process of spinning up a local development database with persistent storage, managed through simple npm scripts.

## ✨ Features

-   **Simple & Fast**: Get a PostgreSQL database running with a single command.
-   **Dockerized**: Encapsulates the database environment, ensuring consistency across different machines.
-   **Persistent Storage**: Uses a named Docker volume to persist your data even after the container is stopped or removed.
-   **Configurable**: Easily configure the database user, password, and name via an environment file.
-   **Healthcheck**: Includes a built-in healthcheck to ensure the database is ready to accept connections.
-   **Script-driven**: Uses npm scripts for easy management (start, stop, and cleanup).

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your system:

-   [Node.js](https://nodejs.org/) (which includes npm)
-   [Docker](https://www.docker.com/products/docker-desktop/)
-   [Docker Compose](https://docs.docker.com/compose/install/)

## 🚀 Getting Started

Follow these steps to get your PostgreSQL instance up and running.

### 1. Clone the Repository

```bash
git clone https://github.com/akshay-bharadva/docker-pg.git
cd docker-pg
```

### 2. Create Environment File

This project uses a `.env.docker-compose` file to manage database credentials. Create this file in the root of the project:

```bash
touch .env.docker-compose
```

Now, open the file and add the following environment variables. Replace the placeholder values with your desired credentials.

**.env.docker-compose**
```env
# PostgreSQL Credentials
POSTGRESQL_USER=myuser
POSTGRESQL_PASSWORD=mysecretpassword
POSTGRESQL_DB_NAME=mydatabase
```

### 3. Start the Database

Run the following command to build and start the PostgreSQL container:

```bash
npm run docker
```

This command will start the container in the foreground, and you will see the PostgreSQL server logs in your terminal. The database will be accessible on `localhost:5432`.

### 4. Connect to the Database

You can now connect to your PostgreSQL instance using any database client (e.g., `psql`, DBeaver, TablePlus, pgAdmin) with the following details:

-   **Host**: `localhost`
-   **Port**: `5432`
-   **Database**: The value of `POSTGRESQL_DB_NAME` from your `.env` file.
-   **User**: The value of `POSTGRESQL_USER` from your `.env` file.
-   **Password**: The value of `POSTGRESQL_PASSWORD` from your `.env` file.


### Start the Service

Starts the PostgreSQL container. Press `Ctrl+C` in the terminal to stop it.

```bash
npm run docker
```

To run the container in the background (detached mode), you can modify the script in `package.json` by adding the `-d` flag:
`"docker": "docker-compose up -d"`

### Stop and Clean Up

Stops the container and removes all associated resources, including the container, network, and the data volume.

```bash
npm run docker:cleanup
```

> **⚠️ Warning:** This command is destructive and will **permanently delete all data** stored in the database volume. Use it with caution.

## 💾 Data Persistence

This setup uses a named Docker volume called `postgres` to store all database data. This ensures that your data is safe and persists across container restarts.

-   To view your Docker volumes, run: `docker volume ls`
-   The data will only be deleted if you run `npm run docker:cleanup` or manually remove the volume with `docker volume rm postgres`.

## 📜 License

This project is licensed under the ISC License. See the `LICENSE` file for details.