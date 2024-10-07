# Step 1: Base image
FROM python:3.10-slim

# Step 2: Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Step 3: Set the working directory
WORKDIR /app

# Step 4: Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Step 5: Copy the requirements file to the container
COPY requirements.txt .
COPY wait-for-it.sh /usr/local/bin/wait-for-it
RUN chmod +x /usr/local/bin/wait-for-it

# Step 6: Install Python dependencies from requirements.txt
RUN pip install --upgrade pip && \
    pip install -r requirements.txt


# Step 8: Expose the port on which the app will run
EXPOSE 8000

# Copy your project files
COPY . .

# Use wait-for-it to wait for the db service
CMD ["wait-for-it", "db:5432", "--", "python", "manage.py", "runserver", "0.0.0.0:8000"]
