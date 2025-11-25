# Netbox Lifecycle Plugin - [netbox-lifecycle](https://github.com/DanSheps/netbox-lifecycle)

## Description	

A netbox plugin providing hardware EOS/EOL, License and Support Contract tracking.

## Use Case	

We have many assets that need to be tracked.

## Requirements
* Netbox 4.1+
* Python 3.10+

## Compatibility

|NetBox Version	| Plugin Version |
|----------------|----------------|
| 3.2.x	| 1.0.0+ |
| 4.1.x | 1.1.3+	|


## Certified	

* Compatible

## Test Priority	

* High
  
## Test Completed	

* Bea 25-11-2025
  
## Evaluation Comments
* The repository/ github page itself has limited information, though I belive the use is fairly straight forward
### Hardware lifecycle
* Assign a hardware lifecycle to device type or module type
* Fill out key dates (end of sale, end of support, etc)
### Support contracts
* Need to have added a vendor, then a contract and then contract assignment
* Support SKUs (stock keeping units?)
### Licensing
* Requires manufacturer

## Review

* 
  
## Next actions

* Does this track everything we need?
* Where is this info currently collated?
* Can it replace the current database/ spreadsheet?


## Installation

Utilise plugins with netbox-docker created by users (within the Netbox Community*) on github by creating a custom 
docker image : https://github.com/netbox-community/netbox-docker/wiki/Using-Netbox-Plugins.


NetBox installed to container (netbox-docker) by creating a custom docker image

### Create and modify files in root folder 
`plugins_requirements.txt`
*  Add plugin `netbox-lifecycle`

`Dockerfile-plugins`

* Dockerfile used to build custom image with plugin - copy in the following.
```
FROM netboxcommunity/netbox:latest

COPY ./plugin_requirements.txt /opt/netbox/
RUN /usr/local/bin/uv pip install -r /opt/netbox/plugin_requirements.txt

# These lines are only required if your plugin has its own static files.
COPY configuration/configuration.py /etc/netbox/config/configuration.py
COPY configuration/plugins.py /etc/netbox/config/plugins.py
RUN DEBUG="true" SECRET_KEY="dummydummydummydummydummydummydummydummydummydummy" \
    /opt/netbox/venv/bin/python /opt/netbox/netbox/manage.py collectstatic --no-input
```

`docker-compose.override.yml`  (already there in netbox docker)
* Ensure the following is added :
```
services:
  netbox:
    image: netbox:latest-plugins
    pull_policy: never
    ports:
      - "8000:8080"
    build:
      context: .
      dockerfile: Dockerfile-Plugins
  netbox-worker:
    image: netbox:latest-plugins
    pull_policy: never

```

### Enable plugin 
`nano configuration/plugins.py`

Add `PLUGINS = ["netbox_lifecycle"]`

Can add plugin configs here also using `PLUGINS_CONFIG`.


### Build and deploy 
```
docker compose build --no-cache
docker compose up -d
```

Navigate to netbox UI and there is now a Topology Views tab in the menu.


## Screenshots

<img width="989" height="717" alt="image" src="https://github.com/user-attachments/assets/6c5f8f75-4582-4537-b321-1c93bcdfca2f" />
