# On Premise Deployment of the AnnoLab Application and Server Cluster

## Overview


This repository contains a docker-compose yml file defining the server cluster setup required for an on-premise deployment. Client & servier images used should explicity use an image tag with the `onprem` verion postfix. E.g. `<IMAGE>:v1.11.14.onprem`. (The database does not follow this pattern)

Making updates to on premise deployments should be done by 1) making a change in the corresponding git repository, 2) pushing a new verison tag containing the `onprem` postfix and 3) Updating the docker-compose file in this repository.


## Configuration

Environment-specific configuration is applied by creating and updating the following files at the root of this project (never commit these files).

`server` -> `configuration file`

1. `db`         -> `conf/db/db.env`         (Template is `db.template.env`)
2. `server`     -> `conf/web-server/web-server.env` (Template is `web-server.template.env`)
3. `client`     -> `conf/web-client/web-client.js`  (Template is `web-client.template.js`)
4. `workers`    -> `conf/workers/workers.env`    (Template is `workers.template.env` )
5. `docker-compose` -> `conf/.docker-compose-env` (Template is `.docker-compose-env.template`)

## Launch

```bash
docker-compose --env-file ./conf/.docker-compose-env up -d
```

## Updating database

TBD

## Auth Configuration

An on-prem deployment most likely uses internal authenication (configurated as AUTH_PROVIDER="AnnoLab"). Do *not* use the client secret defined in the template. Generate a new 64 random character client secret.

On Linux this can be done by using /dev/urandom

```bash
cat /dev/urandom | tr -dc '[:alpha:]' | fold -w ${1:-64} | head -n 1
```

## Nginx Conf

Update the `server_name` records in `conf/nginx/nginx.conf` so that the hostnames match whatever domains the app is being launched under. E.g. `app.<custom-domain>.com` and `api.<custom-domain>.com`.