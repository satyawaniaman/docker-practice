# TypeScript Node.js Server with Docker

A basic TypeScript Node.js server setup for Docker practice.

## Development

```bash
# Install dependencies
npm install

# Run in development mode
npm run dev

# Build the TypeScript code
npm run build

# Run the built code
npm start
```

## Docker Instructions

### Build the Docker image

```bash
docker build -t ts-app .
```

### Run the Docker container

```bash
docker run -p 3000:3000 ts-app
```

### Access the application

- Main endpoint: http://localhost:3000
- Health check: http://localhost:3000/health

## Docker Compose (Optional)

Create a `docker-compose.yml` file:

```yaml
version: "3"
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - PORT=3000
```

Run with Docker Compose:

```bash
docker-compose up
```

## Docker Image Size Comparison

When building your Node.js TypeScript app with different Dockerfile strategies, you can see a significant difference in the final container size:

| Approach          | Dockerfile Used    | Container Name    | Virtual Size |
| ----------------- | ------------------ | ----------------- | ------------ |
| Standard          | Dockerfile.old     | amazing_cray      | 163MB        |
| Multi-stage Build | Dockerfile (multi) | determined_banzai | 129MB        |

- **Standard approach** (Dockerfile.old): Includes all dependencies and build tools, resulting in a larger image size.
- **Multi-stage build** (Dockerfile): Only includes production dependencies and built code, resulting in a smaller, more efficient image.

You can check the size of your running containers using:

```bash
docker ps -s
```

Example output:

```
CONTAINER ID   IMAGE        ...   NAMES               SIZE
...            ts-app       ...   determined_banzai   528B (virtual 129MB)
...            ts-app-old   ...   amazing_cray        528B (virtual 163MB)
```

**Recommendation:** Use multi-stage builds for production to keep your images small and secure.
