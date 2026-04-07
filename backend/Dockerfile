# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Install system dependencies for OpenCV and MediaPipe
RUN apt-get update && apt-get install -y \
    libsm6 \
    libxext6 \
    libxrender-dev \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
# When building from 'backend' as context, this file is at the root
COPY requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy all files from 'backend' into a subdirectory named 'backend'
# This ensures that "import backend.*" works correctly in the code
COPY . ./backend

# Expose the port that FastAPI will run on
EXPOSE 8000

# Command to run the application using uvicorn
# We run it as a module so that 'backend' package is recognized
CMD ["uvicorn", "backend.main:app", "--host", "0.0.0.0", "--port", "8000"]
