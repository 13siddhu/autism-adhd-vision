# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Install system dependencies for OpenCV and MediaPipe
RUN apt-get update && apt-get install -y \
    libgl1 \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
# Now building from project root, so requirements is in 'backend/'
COPY backend/requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy 'backend' and 'src' directories into the container
# This ensures that relative imports like "../../src" from backend work correctly
COPY backend/ ./backend
COPY src/ ./src

# Expose the port that FastAPI will run on
EXPOSE 8000

# Command to run the application using uvicorn
# We run it as a module so that 'backend' package is recognized
CMD ["uvicorn", "backend.main:app", "--host", "0.0.0.0", "--port", "8000"]
