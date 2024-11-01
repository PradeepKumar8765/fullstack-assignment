# Use a lightweight Python image
FROM python:3.10-alpine

# Set the working directory for the container
WORKDIR /app/backend


COPY dependencies.txt .


RUN apk update && \
    apk add --no-cache gcc musl-dev && \
    pip install --no-cache-dir gunicorn

# Install Python dependencies
RUN pip install --no-cache-dir -r dependencies.txt

# Copy the entire project into the container
COPY . .

# Collect static files (if applicable)
RUN python manage.py collectstatic --noinput

EXPOSE 8000

# Start the application with Gunicorn (or the desired command)
CMD ["gunicorn", "backend.wsgi:application", "--bind", "0.0.0.0:8000"]
