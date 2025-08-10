FROM python:3.10-slim

WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt .

# Add matplotlib and pin numpy<2.0 to avoid compatibility issues
RUN pip install --no-cache-dir numpy==1.24.3 \
    && pip install --no-cache-dir -r requirements.txt \
    && pip install --no-cache-dir matplotlib==3.7.1 seaborn==0.12.2

# Copy the application
COPY app_modified.py app.py

# Set environment variables for Matplotlib to avoid permissions issues
ENV MPLCONFIGDIR=/tmp/matplotlib

# Make sure /tmp is writable
RUN mkdir -p /tmp && chmod 777 /tmp

# Make port 7860 available (standard port for Hugging Face Spaces)
EXPOSE 7860

# Define environment variable
ENV PORT=7860

# Run the application
CMD ["streamlit", "run", "--server.port", "7860", "--server.address", "0.0.0.0", "app.py"]