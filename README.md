# Subsocial Starter by [DappForce](https://github.com/dappforce)
Starts entire Subsocial stack with one shell script. 


## Requirements

You should have Linux or macOS with [Docker](https://www.docker.com/get-started) and [Docker Compose](https://docs.docker.com/compose/) installed.

## Get Started

If you're new to Subsocial, it's best to start with the defaults:

```bash
git clone git@github.com:dappforce/dappforce-subsocial-starter.git
cd dappforce-subsocial-starter

./start.sh 
```

## Options

The [start.sh](start.sh) script comes with a set of options for customizing project startup.

| Argument                 | Description                                                                                          |
| ------------------------ | ---------------------------------------------------------------------------------------------------- |
| `--global`               | Binds the project parts to global IP visible on ifconfig.me
| `--force-pull`           | Pull Docker images tagged _latest_ if only `--tag` isn't specified
| `--tag`                  | Specify Docker images tag
| `--prune (all-volumes)`  | Remove the Docker containers. If `all-volumes` is specified, remove volumes as well
| `--no-offchain`          | Start Subsocial stack without offchain storage and Elasticsearch
| `--no-substrate`         | Start Subsocial stack without Substrate node
| `--no-webui`             | Start Subsocial stack without Web UI
| `--only-offchain`        | Start (or update) only offchain container
| `--only-substrate`       | Start (or update) only Substrate node's container
| `--only-webui`           | Start (or update) only Web UI container
| `--substrate-url`        | Specify Substrate websocket URL. Example: `./start.sh --global --substrate-url ws://172.15.0.20:9944`
| `--offchain-url`         | Specify Offchain URL. Example: `./start.sh --global --offchain-url http://172.15.0.3:3001`
| `--elastic-url`          | Specify Elasticsearch cluster URL. Example: `./start.sh --global --elastic-url http://172.15.0.5:9200`
| `--webui-ip`             | Specify Web UI ip address. Example: `./start.sh --global --substrate-url http://172.15.0.2`

### Web UI

By default it will start one container for Web UI. If it is running, you can open the **Subsocial** in your browser:

[http://localhost/](http://localhost)

This one can be managed with `--no-webui` and `--only-webui` flags.

| Container name     | External Port | Local URL        | Description   |
| ------------------ | ------------- | ---------------- | ------------- |
| `subsocial-web-ui` | `80`          | http://localhost | [Subsocial UI](https://github.com/dappforce/dappforce-subsocial-ui)

### Offchain

By default it will start three containers: PostgreSQL, Elasticsearch and offchain (events handler, API) itself.

This one can be managed with `--no-offchain` and `--only-offchain` flags.

| Container name            | External Port   | Local URL                | Description         |
| ------------------------- | --------------- | ------------------------ | ------------------- |
| `subsocial-offchain`      | `3001`          | http://localhost:3001/v1 | [Subsocial Offchain](https://github.com/dappforce/dappforce-subsocial-offchain)
| `subsocial-elasticsearch` | `9200`          | http://localhost:9200    | [Elasticsearch](https://www.elastic.co/what-is/elasticsearch)
| `subsocial-postgres`      |                 |                          | [PostgreSQL](https://www.postgresql.org/about/)

### Substrate Node

By  default it will start two local validator nodes in Docker containers: Alice and Bob. Offchain and others connect to Alice's node, because it's external.

Additional options can be added using `--substrate-extra-opts` (beta).
This one can be managed with `--no-substrate` and `--only-substrate` flags.

| Container name          | External Port   | Local URL             | Description                  |
| ----------------------- | --------------- | --------------------- | ---------------------------- |
| `subsocial-node-alice`  | `9944`          | http://localhost:9944 |
| `subsocial-node-bob`    |                 |                       | Local chain of Substrate Node