[![tests](https://github.com/ochorocho/ddev-mqtt-explorer/actions/workflows/tests.yml/badge.svg?branch=main)](https://github.com/ochorocho/ddev-mqtt-explorer/actions/workflows/tests.yml?query=branch%3Amain)
[![last commit](https://img.shields.io/github/last-commit/ochorocho/ddev-mqtt-explorer)](https://github.com/ochorocho/ddev-mqtt-explorer/commits)
[![release](https://img.shields.io/github/v/release/ochorocho/ddev-mqtt-explorer)](https://github.com/ochorocho/ddev-mqtt-explorer/releases/latest)

# DDEV MQTT Explorer

[MQTT Explorer](https://mqtt-explorer.com/) is a comprehensive MQTT client that provides a structured topic overview. This add-on integrates MQTT Explorer into your [DDEV](https://ddev.com/) project as a web-based UI for visualizing, publishing, and subscribing to MQTT topics.

## Installation

```bash
ddev add-on get ochorocho/ddev-mqtt-explorer
ddev restart
```

After installation, make sure to commit the `.ddev` directory to version control.

## Usage

| Command | Description |
| ------- | ----------- |
| `ddev mqtt-explorer` | Open MQTT Explorer in your browser |
| `ddev describe` | View service status and used ports |
| `ddev logs -s mqtt-explorer` | Check MQTT Explorer logs |

### Default Connection

A default connection profile **"DDEV MQTT Broker"** is pre-configured to connect to `mqtt://web:1883`. This works out of the box if your MQTT broker runs inside the DDEV `web` container. The default is only applied on first launch — any changes you make in the UI are preserved.

### Connecting to an MQTT Broker

MQTT Explorer's web version makes connections from its **Node.js backend** inside the Docker container, not from your browser. Use Docker-internal hostnames, not `localhost`.

### Connecting to a Broker in the Same DDEV Project

If your MQTT broker runs inside the DDEV `web` container (e.g., as a daemon or manual process), the pre-configured default connection should work. If you need to adjust settings:

- **Host**: `web`
- **Port**: `1883` (or your broker's port)
- **Protocol**: `mqtt://`

> **Important**: The broker must bind to `0.0.0.0` (all interfaces), not `127.0.0.1`.
> Loopback-only binding prevents connections from other Docker containers, even though
> host access via `localhost` still works through Docker's port mapping.

### Connecting to an External Broker

For a broker running outside of DDEV, use its public address or IP. If the broker runs on your host machine, use `host.docker.internal` as the hostname.

## Advanced Customization

### Custom Docker Image

To change the Docker image used:

```bash
ddev dotenv set .ddev/.env --mqtt-explorer-docker-image=smeagolworms4/mqtt-explorer:beta
ddev restart
```

## Customization Variables

| Variable | Default |
| -------- | ------- |
| `MQTT_EXPLORER_DOCKER_IMAGE` | `smeagolworms4/mqtt-explorer:latest` |

## Ports

| Service | Port | Protocol | Access |
| ------- | ---- | -------- | ------ |
| MQTT Explorer (HTTP) | 4200 | HTTP | Via DDEV router |
| MQTT Explorer (HTTPS) | 4201 | HTTPS | Via DDEV router |

## Links

- [MQTT Explorer](https://mqtt-explorer.com/) — [GitHub](https://github.com/thomasnordquist/MQTT-Explorer)

## Credits

**Maintained by [@ochorocho](https://github.com/ochorocho)**
