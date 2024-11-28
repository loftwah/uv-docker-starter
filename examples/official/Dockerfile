FROM ghcr.io/astral-sh/uv:python3.13-bookworm

LABEL org.opencontainers.image.source=https://github.com/loftwah/uv-docker-starter
LABEL org.opencontainers.image.description="Official UV Docker Example"
LABEL org.opencontainers.image.licenses=MIT

WORKDIR /app

COPY requirements.txt .
RUN uv pip install --system -r requirements.txt  # Simplified global installation

COPY app/ app/

CMD ["python", "-m", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
