# Lab02: Docker-compatible basics with Podman

## Goal
Use Podman commands that map 1:1 to common Docker workflows, and build confidence with the "daily operations" set: 
**pull / run / ps / exec / logs / stop / rm / rmi / inspect / volume / network**.

## Environment
- macOS: Tahoe 26.3 (Apple Silicon)
- Podman: 5.8.0
- Podman machine: `podman-machine-default`

## Prerequistites
- Podman machine is running:
```bash
podman machine start
```
- Confirm Podman works:
```bash
podman info
```

---

## Tasks (do it yourself)
Do not copy/paste blindly. Type the commands and check results.

### Task 1: Images (pull / list / remove)
1) Pull an image:
```bash
podman pull nginx:1.27
```
2) List images:
```bash
podman pull images
```
3) Remove the image:
```bash
podman rmi nginx:1.27
```

Checkpoint
- You can explain the difference between image and container in 2-3 sentences.

---

### Task 2: Containers (run / ps / logs / stop / rm)
1) Run nginx in the background and expose port 8080 on the host.
  Hint: -d, -p hostPort:containerPort
2) Confirm it is running.
  Hint: podman ps
3) View logs.
  Hint: podman logs <name-or-id>
4) Stop and remove the container.
  Hint: podman stop, podman rm

Checktpoint
- curl http://localhost:8080 returns an nginx response while the container is running.
- After removal, podman ps -a no longer shows it.

---

### Task 3: Exec (enter container and inspect)
1) Start nginx again (same as Task 2).
2) Enter the container.
  Hint: podman exec -it <name-or-id> sh (or bash)
3) Inside the container:
  - Find where nginx serves static files from.
  - Print nginx version.

Checkpoint
- You can write down:
  - the document root path
  - nginx version string

---

### Task 4: Environment variables (-e)
1) Run a container that prints environment variables.
  Constraints: use -e KEY=value
  Hint: use an image that has printenv

Checkpoint
- You can show output that includes your custom env var.

---

### Task 5: Volumes (-v) with bind mount
1) Create a local directory and a simple index.html
2) Run nginx and bind-mount your local directory into nginx document root.
  Constraints: do not rebuild an image
  Hint: -v /path/on/host:/path/in/container:ro
3) Modify index.html locally and confirm the page changes without restarting nginx.

Checkpoint
- You can explain what a bind mount is and when to use it.

---

### Task 6: Inspect (debugging habit)
Pick one of the containers you ran and inspect it:
```bash
podman inspect <name-or-id>
```

Questions
- What is the container IP address?
- What is the mount configuration?
- What is  the entrypoint/cmd?

Checkpoint
- You can point to the exact fields in the JSON output.

---

### Task 7 (optional): Network (user-defined)
1) Create a suer-defined network:
```bash
podman network create lab02-net
```
2) Run two containers on the same network and confitm name-based DNS works.
  Hint: one container runs a simple HTTP server, the other curls it

Checkpoint
- You can show that container A can reach container B by name, not IP.

---

## Reflection (write in your own words)
1) Which comands felt identical to Docker?
2) Waht was different (event slightly)?
3) What do you think Podman's design philosophy is after this lab?

---

## Cleanup (recommended)
```bash
podman ps -a
podman images
```

Only remove things you created for this lab.