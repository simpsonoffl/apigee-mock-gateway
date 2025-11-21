# Apigee Mock Gateway

`apigee-mock-gateway` is a lightweight mock API gateway service that simulates Apigee-like behavior. It helps development and QA teams to mock API endpoints, test integrations, and prototype without needing a real backend.

---

## Table of Contents

- [Overview](#overview)  
- [Motivation](#motivation)  
- [Features](#features)  
- [Architecture](#architecture)  
- [Tech Stack](#tech-stack)  
- [Directory Structure](#directory-structure)  
- [Getting Started](#getting-started)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Running the Service](#running-the-service)  
- [Configuration](#configuration)  
- [Usage](#usage)  
- [Mocking Behavior](#mocking-behavior)  
- [Examples](#examples)  
- [Testing](#testing)  
- [Docker Support](#docker-support)  
- [Contributing](#contributing)  
- [License](#license)  
- [Contact](#contact)

---

## Overview

`apigee-mock-gateway` acts as a proxy server that receives HTTP requests, matches them to mock definitions, and returns pre-configured responses. It is ideal for:

- Frontend development when backend APIs are not yet available  
- Contract testing via mock endpoints  
- Integration testing with stubbed services  
- Simulating gateway behavior (routing, status codes, headers)  

---

## Motivation

- **Parallel development**: Enables frontend and backend teams to work independently.  
- **Integration testing**: Provides a stable, controlled API surface for tests.  
- **Cost and infrastructure reduction**: Avoids the need for full backend or Apigee setup during early stages.  
- **Flexibility**: Easily extend or change mock logic without modifying downstream services.

---

## Features

- HTTP server for mocking API endpoints  
- Custom route matching (path, method)  
- Configurable responses (status code, body, headers)  
- Simulated delays to mimic network latency  
- Easy to extend mock behavior (dynamic logic / rules)  
- Dockerized for local or CI usage

---

## Architecture

┌────────────────────────────┐
│ Client / Consumer │
└─────────────┬───────────────┘
│ HTTP Request
▼
┌────────────────────────────┐
│ Apigee Mock Gateway │
│ - Route Matching │
│ - Response Logic │
│ - Delay Simulation │
└─────────────┬───────────────┘
│
▼
Mock Configuration / Logic

yaml


---

## Tech Stack

- **Language**: Python  
- **HTTP Framework**: (Flask / FastAPI / whichever your code uses)  
- **Configuration Storage**: JSON / Python dicts (or configurable file)  
- **Containerization**: Docker  

---

## Directory Structure

A typical structure for this service may look like:

apigee-mock-gateway/
├── main.py # Entry point for mock gateway
├── config/ # Route config files (JSON / YAML)
├── handlers/ # Custom handlers / logic for mock responses
├── utils/ # Helper functions (delay, matching, etc.)
├── requirements.txt # Python dependencies
└── Dockerfile # Docker setup

yaml


---

## Getting Started

### Prerequisites

- Python 3.7+  
- `pip`  
- Docker (optional but recommended)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/simpsonorg/apigee-mock-gateway.git
   cd apigee-mock-gateway
Create and activate a virtual environment (recommended):

bash
python3 -m venv venv
source venv/bin/activate
Install dependencies:

bash
pip install -r requirements.txt
Running the Service
Run the mock gateway locally:

bash
python main.py
By default, it will listen on a configured port (check your main.py or config).

Configuration
You can configure mock routes by defining them in configuration files (JSON, YAML, or Python modules). Each route definition may include:

Path: e.g., /api/v1/users

HTTP Method: GET, POST, PUT, DELETE, etc.

Response Status Code: e.g., 200, 404

Response Body: JSON or string

Headers: Optional custom headers

Delay: Optional response delay (milliseconds) to simulate latency

Example (JSON):

json
Copy code
{
  "/api/v1/users": {
    "GET": {
      "status": 200,
      "headers": {
        "Content-Type": "application/json"
      },
      "body": [
        { "id": 1, "name": "Alice" },
        { "id": 2, "name": "Bob" }
      ],
      "delay": 100
    },
    "POST": {
      "status": 201,
      "body": { "id": 3, "name": "Charlie" }
    }
  }
}
Usage
Define your mock routes in the configuration file.

Run the mock gateway.

Point your clients or tests to this gateway instead of real backend.

Send HTTP requests as usual, and the gateway will return configured mock responses.

Mocking Behavior
Static responses: Return fixed JSON or text for specific endpoints.

Delayed responses: Add artificial latency (useful for testing timeouts or retries).

Dynamic logic: Build handlers for custom response logic (e.g., based on request parameters or headers).

Examples
GET example:

bash
Copy code
curl http://localhost:5000/api/v1/users
POST example:

bash
Copy code
curl -X POST http://localhost:5000/api/v1/users \
     -H "Content-Type: application/json" \
     -d '{"name": "Charlie"}'
If configured, the mock gateway will respond with a 201 status and the new user object.

Testing
Use pytest (or your preferred test framework) to write tests for your mock definitions.

Validate route matching, response content, and delay behavior.

You can also write integration tests where your frontend or other services hit this mock gateway in CI.

Docker Support
To run the gateway in Docker:

Build the image:

bash
Copy code
docker build -t apigee-mock-gateway .
Run the container:

bash
docker run -p 5000:5000 apigee-mock-gateway
You can pass configuration or environment variables if your main.py supports them.

Contributing
Contributions are very welcome! Here’s how you can help:

Fork this repository

Create a feature branch: git checkout -b feature/my-mock

Define or update mock routes / handlers

Add tests and documentation

Commit changes and push: git commit -m "Add mock route for /foo" → git push origin feature/my-mock

Open a Pull Request

License
This project is licensed under the Citi License.

