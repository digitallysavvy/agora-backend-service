# Agora Go Backend Middleware &nbsp;&nbsp;![go test workflow](https://github.com/digitallysavvy/agora-go-backend-middleware/actions/workflows/go.yml/badge.svg)

The Agora Go Backend Middleware is a microservice that exposes a RESTful API designed to simplify interactions with [Agora.io](https://www.agora.io). Written in Golang and powered by the [Gin framework](https://github.com/gin-gonic/gin), this project serves as a middleware to bridge front-end applications using Agora's Real-Time Voice or Video SDKs with Agora's RESTful APIs.

This middleware streamlines the activation of Agora's extension services, such as Cloud Recording, Real-Time Transcription, and Media Services. To enhance security, the project includes a built-in Token Server with public endpoints, based on the [AgoraIO Community Token Service](https://github.com/AgoraIO-Community/agora-token-service/), ensuring seamless token generation for services requiring Token Security.

## How to Run

Create a `.env` and set the environment variables.

```bash
cp .env.example .env
```

```bash
go run cmd/main.go
```

### Health Check

- GET `/ping`
  - Response: `{"message": "pong"}`

## Micro-Services & Endpoints

```mermaid
flowchart LR
    subgraph Client
        A[HTTP Client]
    end

    subgraph "Gin Web Server"
        B[Router]
    end

    subgraph "Core Services"
        direction TB
        C[Token Service]
        D[Cloud Recording Service]
        E[Real-Time Transcription Service]
        F[RTMP Service]
    end

    subgraph "External"
        K[Agora RESTful API]
    end

    A <-->|Request/Response| B
    B <-->|/token| C
    B <-->|/cloud_recording| D
    B <-->|/rtt| E
    B <-->|/rtmp| F
    D & E & F <-.->|API Calls| K

    classDef request fill:#f9f,stroke:#333,stroke-width:2px;
    classDef response fill:#bbf,stroke:#333,stroke-width:2px;
```

For detailed API specifications, and curl command examples to test the API endpoints locally, please refer to the following pages:

### Token Service

`TokenService` holds the necessary configurations and dependencies for managing tokens.

- [Flow](./DOCS/Architectures/Token_Flow.md)
- [Entity Relationships](./DOCS/Architectures/Token_Entity.md)
- [Endpoints](./DOCS/Endpoints/Token_Endpoints.md)
- [Curl Examples](./DOCS/Local_Testing/Token_curl.md)

### Cloud Recording

`CloudRecordingService` holds the necessary configurations and dependencies for managing cloud recording requests. This includes Cloud Storage for RTT Service

- [Flow](./DOCS/Architectures/Cloud_Recording_Flow.md)
- [Entity Relationships](./DOCS/Architectures/Cloud_Recording_Entity.md)
- [Endpoints](./DOCS/Endpoints/Cloud_Recording_Endpoints.md)
- [Curl Examples](./DOCS/Local_Testing/Cloud_Recording_curl.md)

### Real Time Transcription (RTT)

`RTTService` holds all the necessary configurations and dependencies required for managing real-time transcription requestsħ

- [Flow](./DOCS/Architectures/Real_Time_Transcription_Flow.md)
- [Entity Relationships](./DOCS/Architectures/Real_Time_Transcription_Entity.md)
- [Endpoints](./DOCS/Endpoints/Real_Time_Transcription_Endpoints.md)
- [Curl Examples](./DOCS/Local_Testing/Real_Time_Transcription_curl.md)

### RTMP (Media Push & Pull)

`RTMPService` holds all the necessary configurations and dependencies required for managing media push and cloud player requests.

- [Flow](./DOCS/Architectures/RTMP_Flow.md)
- [Entity Relationships](./DOCS/Architectures/RTMP_Entity.md)
- [Endpoints](./DOCS/Endpoints/RTMP_Endpoints.md)
- [Curl Examples](./DOCS/Local_Testing/RTMP_curl.md)
