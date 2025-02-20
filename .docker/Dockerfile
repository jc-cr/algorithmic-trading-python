# Dockerfile
FROM python:3.8-slim-bookworm

# Avoid prompts from apt
ENV DEBIAN_FRONTEND=noninteractive

# Create a non-root user
RUN useradd -m -s /bin/bash jupyter

# Set environment variables
ENV HOME=/home/jupyter \
    JUPYTER_RUNTIME_DIR=/home/jupyter/.jupyter/runtime \
    JUPYTER_DATA_DIR=/home/jupyter/.jupyter

# Set working directory
WORKDIR /trading_workspace

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    g++ \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements file
COPY .docker/req.txt .

# Install Python packages
RUN pip install --no-cache-dir -r req.txt

# Create Jupyter directories and fix permissions
RUN mkdir -p /home/jupyter/.jupyter/runtime && \
    chown -R jupyter:jupyter /home/jupyter

# Expose Jupyter port
EXPOSE 8888

# Command to run Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.token=''", "--NotebookApp.password=''"]
