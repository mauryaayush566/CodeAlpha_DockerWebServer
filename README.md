# CodeAlpha_DockerWebServer

Nginx web server deployed inside a Docker container (CodeAlpha DevOps Internship – Task 4).

## Project Structure
```
CodeAlpha_DockerWebServer/
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
├── .dockerignore
└── html/
    ├── index.html
    └── 404.html
```

## Run with Docker
```bash
docker build -t codealpha-web .
docker run -d --name codealpha_webserver -p 8080:80 codealpha-web
```
Open: http://localhost:8080

## Run with Docker Compose
```bash
docker compose up -d --build
```

## Container Lifecycle Commands
| Command | Purpose |
|---|---|
| `docker ps` | List running containers |
| `docker logs -f codealpha_webserver` | View logs |
| `docker exec -it codealpha_webserver sh` | Open shell inside container |
| `docker stop codealpha_webserver` | Stop container |
| `docker start codealpha_webserver` | Start container |
| `docker rm -f codealpha_webserver` | Remove container |
| `docker rmi codealpha-web` | Remove image |

## Health Monitoring
```bash
docker inspect --format='{{.State.Health.Status}}' codealpha_webserver
curl http://localhost:8080/health
docker stats codealpha_webserver
```

## Troubleshooting
- **Port already in use:** change `8080` to another port (e.g. `-p 9090:80`).
- **Page not updating:** rebuild with `docker build --no-cache -t codealpha-web .`
- **Container exits:** check `docker logs codealpha_webserver`.

## Best Practices Used
- Small base image (`nginx:alpine`)
- `.dockerignore` to keep image clean
- Pinned image version
- Built-in `HEALTHCHECK`
- Restart policy and security headers
