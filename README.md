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

## Repository Structure

```plaintext
.
├── .github
│   └── workflows
│       └── build-and-push.yml    # GitHub Actions CI/CD workflow
├── LICENSE
├── README.md                     # This documentation file
├── docker-compose.yml            # Local development compose configuration
├── examples
│   ├── custom                    # Custom UV integration example
│   │   ├── Dockerfile
│   │   ├── app
│   │   │   └── main.py
│   │   ├── pyproject.toml       # Project dependencies and metadata
│   │   └── uv.lock             # Locked dependencies for reproducibility
│   └── official                 # Official UV image example
│       ├── Dockerfile
│       ├── app
│       │   └── main.py
│       └── requirements.txt     # Python dependencies
```

## Running the Examples

The repository includes two examples that can run simultaneously:

1. **Official UV Docker Image** (`examples/official`)

   - Uses the official UV Python image
   - Demonstrates simple integration
   - Runs on port 8000

2. **Custom UV Integration** (`examples/custom`)
   - Shows advanced UV integration
   - Uses multi-stage builds
   - Runs on port 8001

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

## CI/CD Pipeline

The repository includes a pre-configured GitHub Actions workflow that automates:

1. Building Docker images for both examples
2. Pushing images to GitHub Container Registry (GHCR)
3. Running automated tests to verify functionality
4. Using build caching for faster deployments

### Workflow Features

- **Multi-stage Builds**: Optimized image sizes
- **Caching**: Faster builds using GitHub Actions cache
- **Automated Testing**: Verifies both services work correctly
- **GHCR Integration**: Automatic pushing of container images
- **Security**: Proper permissions and secret handling

View the workflow: [`.github/workflows/build-and-push.yml`](.github/workflows/build-and-push.yml)

### Container Registry

Images are published to GitHub Container Registry:

- `ghcr.io/[owner]/uv-official:latest`
- `ghcr.io/[owner]/uv-custom:latest`

Each push also creates a SHA-tagged version for immutability.

---

## Development vs CI Testing

The repository uses two compose configurations:

1. `docker-compose.yml` - For local development with build contexts
2. A CI-generated compose file for testing the built images

This separation allows for different workflows in development and CI while maintaining consistent behavior.

---

## Contributing

Feel free to open issues or submit pull requests for improvements or bug fixes. Please ensure:

- Code follows project structure
- Documentation is updated
- Tests pass in CI

---

## License

This repository is licensed under the MIT License. See [LICENSE](LICENSE) for details.
