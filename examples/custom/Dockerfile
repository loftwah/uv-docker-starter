# Build stage
FROM python:3.13-slim-bookworm AS builder

LABEL org.opencontainers.image.source=https://github.com/loftwah/uv-docker-ghcr
LABEL org.opencontainers.image.description="Custom UV Docker Example"
LABEL org.opencontainers.image.licenses=MIT

COPY --from=ghcr.io/astral-sh/uv:latest /uv /usr/local/bin/

WORKDIR /build

COPY pyproject.toml uv.lock ./
RUN uv pip install --system -r pyproject.toml --compile-bytecode

# Final stage
FROM python:3.13-slim-bookworm

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.13/site-packages /usr/local/lib/python3.13/site-packages
COPY app/ app/

CMD ["python", "-m", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
