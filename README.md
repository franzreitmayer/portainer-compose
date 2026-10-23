# Portainer Compose

Portainer CE (Community Edition) als Docker-Compose-Stack.

## Voraussetzungen

- Docker Engine 20.10+
- Docker Compose v2 (`docker compose`)

## Schnellstart

```bash
git clone https://github.com/franzreitmayer/portainer-compose.git
cd portainer-compose
cp .env.example .env   # optional: Ports/Version anpassen
docker compose up -d
```

Danach im Browser öffnen: **https://<server-ip>:9443**

Beim ersten Aufruf wird ein Admin-Benutzer angelegt. Das muss innerhalb von
5 Minuten nach dem Start passieren, sonst sperrt sich Portainer aus
Sicherheitsgründen – dann einfach `docker compose restart portainer` ausführen.

Portainer nutzt ein selbstsigniertes Zertifikat, die Browser-Warnung ist daher normal.

## Konfiguration

| Variable               | Standard | Beschreibung                    |
|------------------------|----------|---------------------------------|
| `PORTAINER_VERSION`    | `lts`    | Image-Tag von `portainer-ce`    |
| `PORTAINER_HTTPS_PORT` | `9443`   | Host-Port der Web-Oberfläche    |
| `PORTAINER_EDGE_PORT`  | `8000`   | Port für Edge-Agents (optional) |

## Betrieb

```bash
docker compose logs -f portainer   # Logs ansehen
docker compose pull && docker compose up -d   # Update
docker compose down                # Stoppen (Daten bleiben erhalten)
```

Die Daten liegen im Volume `portainer_data`. Backup:

```bash
docker run --rm -v portainer_data:/data -v "$PWD":/backup alpine \
  tar czf /backup/portainer_data.tar.gz -C /data .
```
