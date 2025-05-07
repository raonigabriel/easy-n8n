# easy-n8n: Simplified n8n Stack with Docker Compose

This project provides a `docker-compose` configuration to quickly spin up an n8n instance along with several useful companion services, pre-configured with sensible defaults for local development and testing.

---

## ✨ What's Inside?

This stack includes the following services:

*   **n8n:** The core workflow automation tool.
*   **Postgres (with pgVector):** A robust PostgreSQL database, extended with `pgVector` for AI-powered similarity searches and vector embeddings within your n8n workflows.
*   **Minio:** An S3-compatible object storage server, useful for storing binary data, backups, or assets used by your n8n workflows.
*   **Redis:** An in-memory data store, often used for caching, session management, or as a message broker to improve n8n performance in certain scenarios.

## 🚀 Getting Started

### Prerequisites

*   [Docker](https://docs.docker.com/get-docker/)
*   [Docker Compose](https://docs.docker.com/compose/install/)

### Running the Stack

1.  **Clone the repository (or ensure you have the `docker-compose.yml` file).**
2.  **Start the services:**
    Open your terminal in the directory containing the `docker-compose.yml` file and run:
    ```bash
    docker compose up -d
    ```
3.  **Access n8n:**
    Once the containers are up and running, open your web browser and navigate to:
    [http://localhost:5678](http://localhost:5678)

    On your first visit, n8n will guide you through setting up an owner account.

4.  **Stopping the services:**
    To stop all services, run:
    ```bash
    docker compose down
    ```

## ⚠️ Important Disclaimer: Development Use Only

This setup is **NOT INTENDED FOR PRODUCTION USE**.
The default users, passwords, and configurations are **publicly visible** in the `docker-compose.yml` file and are designed for ease of local development only.

For production environments, it is highly recommended to:
*   Secure all credentials (e.g., using environment variables, Docker secrets, or a secrets manager).
*   Implement n8n's [queue mode](https://docs.n8n.io/hosting/scaling/queue-mode/) for scalability.
*   Consider using [task runners](https://docs.n8n.io/hosting/configuration/task-runners/) for distributing workflow executions.
*   Configure proper data persistence and backup strategies.

## 🛠️ Configuration Notes

*   **Port Exposure:** To minimize potential port conflicts with other services running on your host machine, only n8n's port (`5678`) is exposed externally by default.
*   **Inter-Service Communication:** Services within this Docker Compose stack can communicate with each other using their service names as hostnames (e.g., `postgres`, `minio`, `redis`). For example, in n8n, you would connect to PostgreSQL using `postgres` as the host.
*   **Exposing Additional Ports:** If you need to access other services directly from your host machine (e.g., connecting to PostgreSQL on port `5432` with a GUI client), you can uncomment the relevant `ports` section in the `docker-compose.yml` file for that specific service.
    *Example for PostgreSQL:*
    ```yaml
    # services:
    #   postgres:
    #     ports:
    #       - "5432:5432" # Uncomment to expose PostgreSQL
    ```

## 🔑 Default Credentials (For Development Only)

These credentials are set as environment variables in the `docker-compose.yml` file. **Change them if you fork or adapt this for anything beyond local, private testing.**

*   **Minio (S3-compatible storage):**
    *   `MINIO_ROOT_USER`: `minio`
    *   `MINIO_ROOT_PASSWORD`: `CGqz3Kf8`
    *   Access Minio console (if port exposed): `http://localhost:9001` (default Minio console port, not exposed by this stack by default)

*   **Redis:**
    *   `REDIS_PASSWORD`: `CGqz3Kf8`

*   **PostgreSQL (with pgVector):**
    *   `POSTGRES_USER`: `postgres`
    *   `POSTGRES_PASSWORD`: `CGqz3Kf8`
    *   `POSTGRES_DB`: `n8n`
