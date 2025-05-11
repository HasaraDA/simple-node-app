# Simple Node.js Web Application

A basic Express.js web server with Docker support.

## Project Structure

```
simple-node-app/
├── app.js           # Main application file
├── package.json     # Node.js dependencies and scripts
├── Dockerfile       # Instructions for building the Docker image
├── docker-compose.yml # Docker Compose configuration
├── Makefile         # Build automation for Docker images
├── .gitignore       # Git ignore file
└── README.md        # This file
```

## Getting Started

### Running Locally

1. Install dependencies:
   ```
   npm install
   ```

2. Start the server:
   ```
   npm start
   ```

3. The application will be available at: `http://localhost:3000`

### Running with Docker

1. Build the Docker image with tags:
   ```
   # Basic tag
   docker build -t simple-node-app:latest .
   
   # With version tag and build metadata
   docker build \
     --build-arg VERSION=1.0.0 \
     --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') \
     --build-arg VCS_REF=$(git rev-parse --short HEAD) \
     -t simple-node-app:1.0.0 \
     -t simple-node-app:latest .
   ```

2. Run the container:
   ```
   docker run -p 3000:3000 simple-node-app:latest
   ```
   
3. View the image tags and metadata:
   ```
   docker inspect simple-node-app:latest
   ```

3. The application will be available at: `http://localhost:3000`

## Development

For development with automatic restart on code changes:

```
npm run dev
```

## Docker Image Tagging

This project includes several options for building and tagging Docker images:

### Using Docker Directly

```bash
# Basic tag
docker build -t simple-node-app:latest .

# With version and metadata
docker build \
  --build-arg VERSION=1.0.0 \
  --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') \
  --build-arg VCS_REF=$(git rev-parse --short HEAD) \
  -t simple-node-app:1.0.0 .
```

### Using Docker Compose

```bash
# Build and run with default tags
docker-compose up -d

# Build with custom version and tag
VERSION=2.0.0 TAG=v2.0.0 docker-compose build
```

### Using Makefile

```bash
# Build with default version (1.0.0)
make build

# Tag the image
make tag

# Build, tag, and run
make build tag run

# Clean up images
make clean
```