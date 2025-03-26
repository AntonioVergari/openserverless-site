---
title: Runtimes
description: OpenServerless' supported runtimes
#weight: 60
draft: false
---

# Apache OpenServerless (OPS) Runtimes Explained

Apache OpenServerless (OPS) is a serverless platform built on Apache OpenWhisk, designed to execute functions in a scalable, event-driven environment. OPS leverages OpenWhisk's runtime model while extending its capabilities to support additional customization via Docker.

---

## Overview of OPS Runtimes

A **runtime** in OPS is a preconfigured environment that executes a serverless function.
Since serverless platforms allocate compute resources dynamically, a runtime ensures:

1. **Portability** – Developers can write code in different languages without managing dependencies.
2. **Scalability** – The system provisions and scales runtimes automatically based on demand.
3. **Isolation** – Each Action runs within its own dedicated runtime environment, ensuring security and consistency.
4. **Resource Efficiency** – The platform optimizes resource allocation by suspending inactive runtimes and reusing active ones when possible.

OPS natively supports the following runtimes:
- **Python**
- **Node.js**
- **PHP**

However, since OPS is built on OpenWhisk, it inherits compatibility with all [OpenWhisk-supported runtimes](https://openwhisk.apache.org/documentation.html#runtimes) (e.g., Java, Go) and allows users to define custom runtimes using Docker containers.

For greater flexibility, developers can also package their own runtime environments using Docker to create "black box" actions.

---

## How OPS Runtimes Work

### 1. Runtime Lifecycle
OPS follows OpenWhisk's runtime model, where each function invocation occurs in an isolated container. The lifecycle includes:
1. **Initialization**: A container is provisioned with the selected runtime.
2. **Execution**: The function code runs within the container.
3. **Idle**: The container is paused (but retained) for reuse (Warm Start).
4. **Destroying**: Idle containers are garbage-collected after a timeout.

### 2. Cold vs. Warm Starts
- **Cold Start**: A new container is created, increasing latency.
- **Warm Start**: Reuses a paused container for faster execution.

### 3. Runtime Composition
Each runtime includes:
- **Language Interpreter/Compiler**: (e.g., Python 3.12, Node.js 21).
- **OpenWhisk-Compatible Bootstrap**: A script that listens for triggers and invokes the function.
- **Dependencies**: Preinstalled libraries (e.g., `requests` for Python).

---

## Supported Runtimes

### 1. Native OPS Runtimes
| Runtime   | Version      | Entrypoint       |
|-----------|--------------|------------------|
| Python    | 3.12         | `__main__.py`    |
| Node.js   | 21.x         | `index.js`       |
| PHP       | 8.3          | `index.php`      |

### 2. OpenWhisk-Compatible Runtimes
OPS supports all OpenWhisk runtimes, including:
- Java (JDK 11)
- Go (1.18)
- Ruby (3.0)
- .NET Core (3.1)

