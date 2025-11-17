A plugin to allow the ability to reorder rack units in NetBox using a drag and drop interface. 

### Environment
Tested on google cloud virtual machine (test1) using netbox docker. 
Tested install alongside topology plugin to test multiple plugins and reinforce installation with NetBox docker.

# Installation

`nano plugin_requirements.txt` add netbox-reorder-rack

`Dockerfile-Plugins` No need to update as file already exists (from topology install). This Dockerfile is used to build the custom image, 
it points to the plugin_requirements.txt and plugin.py files which will have the relevant information about which plugin
is being installed.

`docker-compose.override.yml` Same as above, already correct to point to the files which we need to update and use to configure the custom docker image.


Add plugin to `configuration/plugins.py`
```
PLUGINS = ["netbox_reorder_rack"]
```

## Build and deploy
```
docker compose build --no-cache
docker compose build up -d
```

Navigate to http://34.39.10.82:8000 to check it is working. SUCCESS.

# Review

* Smooth, works well
* Very handy for rearranging, but perhaps won't be used much? I am unsure how often thuis occurs but also it doesn't harm having the plugin available when needed?
* Has a separate 'unracked devices' section for devices not currently assigned to a rack/slot

