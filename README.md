# Overleaf Toolkit

(Note: this software is currently in beta testing. Functionality and documentation
may be incomplete)

This repository contains the Overleaf Toolkit, the standard tools for running a local
instance of [Overleaf](https://overleaf.com). This toolkit will help you to set up and administer both Overleaf Community Edition (free to use, and community supported), and Overleaf Server Pro (commercial, with professional support).


## Getting Started

Clone this repository locally:

``` sh
git clone https://github.com/overleaf/toolkit.git overleaf-toolkit
```

Then follow the [Quick Start Guide](./doc/quick-start-guide.md).


## Documentation

See [Documentation Index](./doc/index.md)


## Getting Help

Users of the free Community Edition should [open an issue on github](https://github.com/overleaf/toolkit/issues). 

Users of Server Pro should contact `support@overleaf.com` for assistance.



## Config files

- `config/overleaf.rc`
- `config/variables.env`
- `config/version`

If `config/docker-compose.override.yml` is present, it will also be loaded.


## Docker Compose files

- `lib/docker-compose.base.yml`
- `lib/docker-compose.mongo.yml`
- `lib/docker-compose.redis.yml`
- `lib/docker-compose.sibling-containers.yml`


### overleaf.rc

The `config/overleaf.rc` file controls top-level configuration,
such as the docker image to use, data paths, etc. This is used
to configure the invocaton to docker-compose.


### variables.env

Environment variables loaded in the overleaf container as application
settings.


## Data directories (default)

- `data/mongo`
- `data/redis`
- `data/sharelatex`

All are persisted outside of the containers. 

These can be changed by setting `MONGO_DATA_PATH` (etc) in `overleaf.rc`


## How To 

### Update to the latest version

- Run `bin/upgrade`, and follow the instructions
  - This will fetch any available code updates and offer to upgrade the
    locally configured docker image version, if a new version is available


### Switch to Server Pro

- In `overleaf.rc`, set `SERVER_PRO=true`


### Change Image

- Change the contents of `config/version`


### Using an external mongo/redis

- Mongo
  - Set `MONGO_ENABLED=false`, and `MONGO_URL=...` in `overleaf.rc`
- Redis
  - Set `REDIS_ENABLED=false`, and `REDIS_HOST=...` and/or `REDIS_PORT=...` in `overleaf.rc`


### Using Sibling-Containers

- In `overleaf.rc` set `SIBLING_CONTAINERS_ENABLED=true`
- In `overleaf.rc`, ensure `DOCKER_SOCKET_PATH` is set
