# backend/product_service/Dockerfile
FROM python:3.11-slim

# Create non-root user for safety (optional)
RUN adduser --disabled-password --gecos "" appuser

WORKDIR /app

# Install system deps (if needed)
RUN apt-get update && apt-get install -y build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy app code (assumes code in ./app)
COPY ./app ./app

# Use non-root user
USER appuser

EXPOSE 80

# Run uvicorn; adjust app module if different
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
