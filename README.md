# On Premise Deployment of the AnnoLab Application and Server Cluster

## Overview


This repository contains a docker-compose yml file defining the server cluster setup required for an on-premise deployment. Client & servier images used should explicity use an image tag with the `onprem` verion postfix. E.g. `<IMAGE>:v1.11.14.onprem`. (The database does not follow this pattern)

Making updates to on premise deployments should be done by 1) making a change in the corresponding git repository, 2) pushing a new verison tag containing the `onprem` postfix and 3) Updating the docker-compose file in this repository.

## Configuration

Environment-specific configuration is applied by creating and updating the following files at the root of this project (never commit these files).

`server` -> `configuration file`

1. `db`         -> `db.env`         (Template is `db.template.env`)
2. `web-server` -> `web-server.env` (Template is `web-server.template.env`)
3. `web-client` -> `web-client.js`  (Template is `web-client.template.js`)