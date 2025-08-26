# Go Microservices Demo

A demonstration of microservices architecture in Go, featuring service discovery with Consul and an API Gateway for request routing.

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue?style=for-the-badge&logo=github)](https://github.com/KeldenPDorji/AS2025WEB303/blob/main/Practicals/Practical_2/README.md)

## Architecture

- **API Gateway** (Port 8080) - Routes requests to microservices
- **Users Service** (Port 8081) - Handles user operations
- **Products Service** (Port 8082) - Handles product operations
- **Consul** - Service discovery and health checking

## Quick Start

### Prerequisites
- Go 1.24.5+
- Consul

### Setup
```bash
# Install Consul (macOS)
brew install consul

# Clone and setup
git clone https://github.com/KeldenPDorji/go-microservices-demo.git
cd go-microservices-demo
```

### Run
```bash
# Terminal 1: Start Consul
consul agent -dev

# Terminal 2: Start Users Service
cd services/users-service && go run main.go

# Terminal 3: Start Products Service  
cd services/products-service && go run main.go

# Terminal 4: Start API Gateway
cd api-gateway && go run main.go
```

## Usage

```bash
# Test endpoints
curl http://localhost:8080/api/users/123/products
curl http://localhost:8080/api/products/456

# Check health
curl http://localhost:8081/health
curl http://localhost:8082/health

# View Consul UI
open http://localhost:8500
```

## How It Works

1. Services register with Consul on startup
2. API Gateway discovers services via Consul
3. Requests to `/api/users/*` route to users-service
4. Requests to `/api/products/*` route to products-service
5. Consul monitors service health via `/health` endpoints

## Tech Stack

- **Go** - Programming language
- **[Chi Router](https://github.com/go-chi/chi)** - HTTP routing
- **[Consul](https://github.com/hashicorp/consul/api)** - Service discovery
