# Lab01: Hello Podman

## Goal
Run a container with Podman and confirm the setup works on macOS (Apple Silicon).

## Environment
- macOS: Tahoe 26.3
- CPU: Apple Silicon (M1)
- Podman: 5.8.0

## Setup (one-time)
### 1) Create and start the Podman machine
```bash
podman machine init
podman machine start
```
### 2) Verify Podman is working
```bash
podman info
```
## Run
```bash
podman run --rm quay.io/podman/hello
```