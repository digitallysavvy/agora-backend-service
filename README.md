# Agora Middleware Webservice

The Agora Middleware Webservice is a RESTful API designed to simplify interactions with [Agora.io](https://www.agora.io). Written in Golang and powered by the [Gin framework](https://github.com/gin-gonic/gin), this project serves as a middleware to bridge front-end applications using Agora's Real-Time Voice or Video SDKs with Agora's RESTful APIs.

This middleware streamlines the activation of Agora's extension services, such as Cloud Recording, Real-Time Transcription, and Media Services. To enhance security, the project includes a built-in Token Server with public endpoints, based on the [AgoraIO Community Token Service](https://github.com/AgoraIO-Community/agora-token-service/), ensuring seamless token generation for services requiring Token Security.

## How to Run

Create a `.env` and set the environment variables.

```bash
cp .env.example .env
```

```bash
go run cmd/main.go
```

## Endpoints

- [GET /ping]()
- [POST /token/getNew]()
- [POST /cloudrecording/start]()
- [POST /cloudrecording/stop]()
- [GET /cloudrecording/status]()
- [POST /cloudrecording/update/subscriber-list]()
- [POST /cloudrecording/update/layout]()
