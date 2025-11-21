# Apigee Mock Gateway

A simple mock gateway built using Python to simulate Apigee-like behavior for API development and testing.

## Table of Contents

- [Motivation](#motivation)  
- [Features](#features)  
- [Architecture](#architecture)  
- [Getting Started](#getting-started)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Running](#running)  
  - [Configuration](#configuration)  
- [Usage](#usage)  
- [Examples](#examples)  
- [Testing](#testing)  
- [Contributing](#contributing)  
- [License](#license)  
- [Contact](#contact)  

---

## Motivation

When building API-driven applications, frontend teams and integration testers often need a stable API layer before the real backend is ready. This mock gateway:

- Helps frontend/backend teams work in parallel.  
- Supports integration testing without relying on actual APIs.  
- Emulates basic Apigee API Gateway behavior, making development more robust and predictable.

---

## Features

- HTTP mock server implemented in Python (using `main.py`).  
- Configurable routes and responses to simulate realistic API behavior.  
- Containerized using Docker for ease of deployment.  
- Lightweight and easy to extend for custom mocking needs.

---

## Architecture

Here’s a high-level view:

1. **Python App** (`main.py`) handles incoming HTTP requests.  
2. It matches the request to predefined routes and returns mock responses.  
3. You can run the server locally or inside a Docker container.  
4. The gateway does not enforce full Apigee policy logic (like security, quotas) — it’s a **mock** for development/testing.

---

## Getting Started

### Prerequisites

- Python 3.8+  
- `pip` (or `pipenv` / `virtualenv`)  
- Docker (if you want to run via container)  

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/simpsonorg/apigee-mock-gateway.git
   cd apigee-mock-gateway

2.Create a virtual environment:

python3 -m venv venv
source venv/bin/activate

3.Install dependencies:

pip install -r requirements.txt

