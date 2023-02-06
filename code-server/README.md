# Code-Server

[![Docker Repository on Quay](https://quay.io/repository/komish/code-server/status "Docker Repository on Quay")](https://quay.io/repository/komish/code-server)

Set up a quick development environment in a container for when you can't get
your local system set up how you want. This is built on Fedora images.

The Upstream Project is https://github.com/coder/code-server.

# Build

```bash
VERS=4.9.1 # change based on https://github.com/coder/code-server/releases/
podman build -t quay.io/komish/code-server:${VERS}-fedora --build-arg VERSION=${VERS} .
```

# Run (sample)

Note: The below command runs the application without authentication. Make sure
you adjust your port publishing stance, or your authentication state as relevant
to your environment.

```bash
VERS=4.9.1
podman run -it --rm --hostname devcontainer -p 8989:8080 quay.io/komish/code-server:${VERS}-fedora code-server --disable-telemetry --auth none --bind-addr 0.0.0.0:8080 /home/coder/
```