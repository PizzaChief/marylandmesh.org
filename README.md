# marylandmesh.org
Maryland Mesh — A community resource for Meshtastic, LoRa, node configuration, and local mesh networking.

## Maryland network monitor

The active Maryland live map, node list, and network activity are provided by
[`monitor.marylandmesh.org`](https://monitor.marylandmesh.org/). The homepage
links directly to that dashboard; the static Leaflet prototype and its local
`nodes.json` data file have been retired.

The dashboard deployment package is in `deploy/potato-mesh/`. It uses the
upstream PotatoMesh web and ingestor images. Review the deployment notes there
for service and ingestor setup.

## MeshCore

Maryland Mesh also links to the separate MeshCore project and its official
guides and map. MeshCore uses its own firmware, apps, and network; see
https://meshcore.io/docs for current setup information.
