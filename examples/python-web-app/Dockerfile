FROM ubuntu:noble

# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /app

# Install required OS packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        python3 \
        python3-pip \
        python3-venv \
        apt-utils \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy app files
COPY requirements.txt /app
COPY devops /app/devops

# Create and activate virtual environment
RUN python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install -r requirements.txt

# Set the path so `python` and `pip` point to the venv
ENV PATH="/app/venv/bin:$PATH"

# Run the app
ENTRYPOINT ["python3"]
CMD ["devops/manage.py", "runserver", "0.0.0.0:8000"]
