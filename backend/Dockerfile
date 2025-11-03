FROM python:3.11-slim

WORKDIR /app

# Install system dependencies and certificates
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        gcc \
        curl \
        ca-certificates \
        libssl-dev \
        libffi-dev && \
    update-ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Force Python to use updated certifi trust store
ENV SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt

# Upgrade pip etc safely
RUN python -m pip install --upgrade --trusted-host pypi.org --trusted-host files.pythonhosted.org pip setuptools wheel

# Copy requirements first
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir \
    --trusted-host pypi.org \
    --trusted-host pypi.python.org \
    --trusted-host files.pythonhosted.org \
    -r requirements.txt

# Copy rest of app
COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
