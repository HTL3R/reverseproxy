# Reverse Proxy mit nginx und Docker Compose

Ausgangs-Setup: nginx als Reverse Proxy vor zwei Backends.

| Service         | Image               | Port                  |
|-----------------|---------|-----------------------|
| `reverse-proxy` | `nginx` | 8080 am Host          |
| `backend-a`     | `nginx` | 80, nur intern        |
| `backend-b`     | `nginx` | 80, nur intern        |

## Starten

```bash
docker compose up -d
```

## Testen

```bash
curl http://localhost:8080/service/a   # -> Reverse Proxy Target A
curl http://localhost:8080/service/b   # -> Reverse Proxy Target B
curl http://localhost:8080/healthz     # -> ok
```

## Änderungen übernehmen

- nach Änderungen an `proxy/nginx.conf`: `docker compose restart reverse-proxy`
- nach Änderungen an `docker-compose.yml`: `docker compose up -d`

## Struktur

```
docker-compose.yml   Services
proxy/nginx.conf     Konfiguration des Reverse Proxy
backends/a, b        Inhalte der Backends
docs/                Nachweise und Antworten
```
