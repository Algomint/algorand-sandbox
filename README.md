# algorand-sandbox

Creates a Algorand private network including Algod and Indexer REST APIs.

This work is based on the original [Algorand Sandbox](https://github.com/algorand/sandbox), but modified so that it runs directly under Docker/Docker-Compose under a Windows terminal.

To use this on Windows you need [Docker installed under WSL2](https://docs.docker.com/desktop/windows/install/).

This Sandbox is also deployable to a Kubernetes cluster, allowing your team to host their Sandbox(s) in the cloud.

## Getting this repo

Clone the repo:

```bash
meta git clone git@github.com:hone-labs/algorand-sandbox.git
```

## Important end points

- Algo-proxy: http://localhost:4000
- Algod REST API: http://localhost:4001
- Indexer REST API: http://localhost:8980

## Running the backend

To bring up all services:

```bash
docker compose up --build
```

Doing a full build takes quite a while because it fetches fresh code code from the Algorand code repositories.

You can omit `--build` to start quickly from cached images:

```bash
docker compose up
```

To shutdown:

```bash
docker compose down
```

## Testing APIs

Open requests (.http) files in `./api-tester`. 

Have VS Code REST Client installed.

Run individual requests to test the local sandbox.

## Shell into the Algod container

```bash
docker exec -it algorand-sandbox-algod /bin/bash
````

To work with shared files:

```bash
cd /shared
```

Once you have a shell into algod you can run goals commands against it, like:

```bash
goal account list
```

## Changing to "dev mode"

Open `docker-compose.yml`.

Change this line:

```
ARG TEMPLATE="/tmp/images/algod/template.json"
```

To use the dev template:

```
ARG TEMPLATE="/tmp/images/algod/dev-template.json"
```

Restart:

```
docker compose down
docker compose up
```