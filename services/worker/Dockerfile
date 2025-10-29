# Imagen base con CUDA 11.8 para que vLLM y Torch 2.6.0 funcionen
FROM nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu22.04
# Python y utilidades
RUN apt-get update && apt-get install -y python3.12 python3.12-venv python3-pip && rm -rf /var/lib/apt/lists/*
WORKDIR /workspace
COPY requirements.txt .
# vLLM nightly trae soporte DeepSeek-OCR upstream
RUN pip3 install --no-cache-dir -r requirements.txt
COPY worker ./worker
ENV PYTHONUNBUFFERED=1
CMD ["bash", "-lc", "python3 -m celery -A worker.ocr_worker worker --loglevel=INFO"]