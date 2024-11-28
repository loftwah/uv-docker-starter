# UV Docker Starter

This repository provides examples of integrating the blazing-fast UV Python package manager into Docker-based workflows. It includes both a quick-start approach using **official UV images** and a **custom integration** approach optimized for production use.

## Features

- Examples for **official UV images** and **custom UV integration**
- Docker Compose setup for running both examples simultaneously
- Multi-platform support (Linux `amd64`, `arm64`)
- Pre-configured CI/CD pipeline with GitHub Actions
- Secure, optimized, and reproducible builds

---

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/loftwah/uv-docker-starter.git
cd uv-docker-starter
```

### Prerequisites

- Docker version 20.10 or higher
- Docker Compose version 2.x or higher
- Python 3.13 (optional, for local testing)
- At least 4GB of RAM and 10GB of free disk space

Check your versions:

```bash
docker --version
docker compose version
python --version
```

---

## Running the Examples

The repository includes two examples that can run simultaneously:

1. **Official UV Docker Image** (`examples/official`)
2. **Custom UV Integration** (`examples/custom`)

### Run Both Examples with Docker Compose

Use Docker Compose to build and run both services simultaneously:

```bash
docker compose up --build
```

#### Test the Services

Once the containers are running, use `curl` or any HTTP client to test both services.

- **Official Example (Port 8000):**

  ```bash
  curl localhost:8000
  ```

  **Expected Output:**

  ```json
  { "message": "Hello, UV Official Image!" }
  ```

- **Custom Example (Port 8001):**

  ```bash
  curl localhost:8001
  ```

  **Expected Output:**

  ```json
  { "message": "Hello, UV Custom Integration!" }
  ```

#### Stop the Services

When you're done, stop the containers:

```bash
docker compose down
```

---

## CI/CD Workflow

The repository includes a pre-configured GitHub Actions workflow that automates:

1. Building and pushing Docker images to GitHub Container Registry (GHCR)
2. Running tests to verify functionality
3. Supporting multi-platform builds (`amd64`, `arm64`)

View the workflow: [`.github/workflows/build-and-push.yml`](.github/workflows/build-and-push.yml)

---

## Repository Structure

```plaintext
uv-docker-starter/
├── README.md               # Guide and instructions
├── docker-compose.yml      # Compose configurations for examples
├── examples/
│   ├── official/           # Example using official UV Docker image
│   │   ├── Dockerfile
│   │   ├── app/
│   │   │   └── main.py
│   │   └── requirements.txt
│   ├── custom/             # Example with custom UV integration
│   │   ├── Dockerfile
│   │   ├── pyproject.toml
│   │   ├── uv.lock
│   │   └── app/
│   │       └── main.py
├── .github/
│   ├── workflows/
│   │   └── build-and-push.yml # CI/CD pipeline for GitHub Actions
```

---

## Testing

You can test both services simultaneously using the following commands:

- **Official Example (Port 8000):**

  ```bash
  curl localhost:8000
  ```

  **Expected Output:**

  ```json
  { "message": "Hello, UV Official Image!" }
  ```

- **Custom Example (Port 8001):**

  ```bash
  curl localhost:8001
  ```

  **Expected Output:**

  ```json
  { "message": "Hello, UV Custom Integration!" }
  ```

---

## Contributing

Feel free to open issues or submit pull requests for improvements or bug fixes.

---

## License

This repository is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---
