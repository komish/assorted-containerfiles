# Pocketbase

Container Image for PocketBase: Open Source Backend for your applications

Project: https://pocketbase.io/

## Quickstart - Run App

The application runs from /pocketbase and creates a few directories there. It's
intended to run using a single-file sqlite backend, so you'll probably want to
mount a host filesystem at this path to persist that data cross rebuilds.

```shell
podman run -it --publish 8090:8090 -v /host/pocketbase/app/dir:/pocketbase:z quay.io/komish/pocketbase:latest serve --http 0.0.0.0:8090
```

## Quickstart - Build Image

```shell
imageref="example.com/namespace/image:tag"

podman build -t "${imageref}" . --build-arg=VERSION=0.12.1  # latest version as of this publishing.
```