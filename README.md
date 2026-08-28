# FleetOps - API Gateway

Part of the **FleetOps Fleet & Logistics Dispatch System**, submitted for the
Enterprise Cloud Architecture (ITS 2130) capstone project.

## Student Information
- **Name:** K.D. Chanuth Dewhan
- **Student ID:** 241722017
- **Slack Handle:** @chanuthdewhan
- **GCP Project ID:** fleet-ops-506803

## Project Description
The single entry point for all external traffic into the FleetOps system,
built on Spring Cloud Gateway. Routes incoming requests to the correct
downstream microservice (Order & Dispatch, Trip & Telemetry, Notification)
based on the request path, using Eureka service discovery for load-balanced
routing. A custom global filter validates JWT tokens on every request except
login and registration, forwarding the authenticated user's identity to
downstream services via headers so that individual services never need to
re-implement token validation themselves.

## Technology Stack
- Java 25
- Spring Boot 4.1
- Spring Cloud 2025.1.2 — Gateway (WebFlux), Eureka Client, Config Client
- JWT (jjwt)

## Setup / Getting Started

```bash
git clone https://github.com/chanuthdewhan/fleetops-api-gateway.git
cd fleetops-api-gateway
./mvnw spring-boot:run
```

Runs on port `7000` locally. Requires `fleetops-service-registry` and
`fleetops-config-server` to be running first.

## Key Behavior
- Public endpoints: `/api/v1/auth/login`, `/api/v1/auth/register`
- All other endpoints require a valid `Bearer` JWT token
- Routes `/api/v1/orders/**`, `/api/v1/customers/**`, `/api/v1/drivers/**`,
  `/api/v1/vehicles/**`, `/api/v1/auth/**` to Order & Dispatch Service
- Routes `/api/v1/trips/**` to Trip & Telemetry Service
- Routes `/api/v1/notifications/**` to Notification Service

## Live Deployment
- **GCP Project ID:** fleet-ops-506803
- **Region:** asia-southeast1
- **Deployment model:** IaaS — Compute Engine, managed via PM2
- **Public URL:** http://34.21.225.166:80