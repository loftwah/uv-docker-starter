# UV Docker with GHCR

This repository demonstrates building and pushing container images for UV examples to **GitHub Container Registry (GHCR)**.

## Examples

### 1. Official UV Image

The `uv-official` image demonstrates using the official UV Docker image.

### 2. Custom UV Integration

The `uv-custom` image uses a custom integration for optimized builds.

## Running Locally

### Use Bash Scripts

You can use the provided bash scripts to build and run each example:

#### Build and run the `official` example:

```bash
./build-official.sh
```

#### Build and run the `custom` example:

```bash
./build-custom.sh
```

### Use Docker Compose

To run both examples simultaneously:

```bash
docker compose up
```

Access the services:

- Official: [http://localhost:8000](http://localhost:8000)
- Custom: [http://localhost:8001](http://localhost:8001)

## How the Images Are Built

### Official Example (`uv-official`)

- **Dependencies** are defined in `examples/official/requirements.txt`.
- **Dependencies** are installed globally using `uv pip install --system -r requirements.txt`.
- The application (`examples/official/app/main.py`) is served via `uvicorn`.

### Custom Example (`uv-custom`)

- Uses `examples/custom/pyproject.toml` to define dependencies.
- Dependencies are installed using `uv pip install --system`.
- The application (`examples/custom/app/main.py`) is served via `uvicorn`.

### Multi-Platform Build

Both examples are configured for multi-platform builds (e.g., `linux/amd64`, `linux/arm64`) using Docker Buildx. This is enabled in both the CI workflow and the provided bash scripts.

## Automated Workflow

On each push to the `main` branch, GitHub Actions:

1. Builds the Docker images for both examples using Buildx.
2. Pushes the images to GHCR:
   - `ghcr.io/loftwah/uv-official:latest`
   - `ghcr.io/loftwah/uv-custom:latest`

## Troubleshooting

1. **Build Errors for `uv-official`:**
   Ensure `requirements.txt` exists in the `examples/official` directory.

2. **Build Errors for `uv-custom`:**
   Ensure `pyproject.toml` and `uv.lock` exist in the `examples/custom` directory.

3. **Check Logs:**
   Run `docker compose logs` for detailed error information.

4. **Rebuild Images:**
   If issues persist, rebuild images:
   ```bash
   docker compose build
   ```

## Next Steps

1. Extend the examples to include more complex applications.
2. Customise the CI/CD workflow to deploy built images.
3. Optimise the Dockerfiles for production-ready configurations.

---
