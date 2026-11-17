# Maryland Mesh Monitor deployment

This runs the upstream PotatoMesh dashboard as a separate service from the
GitHub Pages website. It includes the full map, node list, node details,
telemetry, activity views, and API. The image is pinned to the upstream v1.0.0
release; PotatoMesh is Apache-2.0 licensed.

## Server setup

1. Use a Linux host with Docker Compose. Create DNS for
   `monitor.marylandmesh.org` pointing to that host.
2. Copy this directory to the host, copy `.env.example` to `.env`, and replace
   `API_TOKEN` with a unique secret. Do not commit `.env` or share the token in
   the public website repository.
3. Configure the host's existing HTTPS reverse proxy to send
   `monitor.marylandmesh.org` to `127.0.0.1:41447`. The service binds only to
   localhost so the proxy can terminate TLS.
4. Start the dashboard with `docker compose up -d`.

The dashboard can run before a radio ingestor is connected. It will show the
map and dashboard shell while waiting for node reports.

## Optional Meshtastic ingestor

To collect data from a node that exposes a reachable TCP API, set `CONNECTION`
in `.env` to its address (for example `192.168.1.20:4403`) and start with
`docker compose --profile ingestor up -d`. The ingestor connects to the node
and sends data to the web service using the private API token. The ingestor is
receive-only by default. The included profile does not pass radio transmissions
through to the mesh.

Additional volunteer ingestors can run separately and point at the same
dashboard API, but each needs secure access to the API token. For a public
volunteer program, plan separate credentials or another ingestion gateway
before distributing a shared token broadly.

## Website link

The MarylandMesh website links its map and coverage navigation to
`https://monitor.marylandmesh.org/`, which is the active dashboard. Keep its
DNS and HTTPS endpoint available when changing the monitor deployment.
