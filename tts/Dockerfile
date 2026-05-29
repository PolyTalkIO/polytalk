FROM python:3.12-slim

ENV PIP_BREAK_SYSTEM_PACKAGES=1

WORKDIR /app

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    ninja-build \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install Piper TTS and Gunicorn
RUN pip install --no-cache-dir piper-tts[http] gunicorn

# Copy service application
COPY wsgi.py /app/wsgi.py

# Copy voices directory
COPY voices/ /data/

EXPOSE 5000

CMD ["sh", "-c", "exec gunicorn --bind 0.0.0.0:5000 --workers ${TTS_WORKERS:-4} wsgi:app"]
