Netbox plugin to create topology views/maps from your devices in Netbox. The connections based on the cables created in Netbox.

## Install
* https://github.com/netbox-community/netbox-docker/wiki/Using-Netbox-Plugins
* Installed to container (Netbox-Docker)
* Custom docker image created

### Create and modify files in root folder 
`plugins_requirements.txt`
*  Add plugin `netbox-topology-views`

`Dockerfile-plugins`

* Dockerfile used to build custom image with plugin
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

Add `PLUGINS = ["netbox_topology_views"]`

Can add plugin configs here also using `PLUGINS_CONFIG`.

The following allows for fixed and saved coordinates making layouts much nicer and easier to manipulate topology clearly.
```
PLUGINS_CONFIG = {
   "netbox_topology_views": {
        'allow_coordinates_saving': True,
        'always_save_coordinates': True
   }
 }
```

### Build and start 
```
docker compose build --no-cache
docker compose up -d
```

Navigate to netbox UI and there is now a Topology Views tab in the menu.

### Success with TLE populated server
### Success with demo data (v4.4) 
### Success with Telent mini data
Using the plugin configurations to allow for coordinate saving, it is possible to rearrange map data into a fixed pattern to make diagrams clear and organised.

For example a section of MMLite : 
<img width="1345" height="644" alt="image" src="https://github.com/user-attachments/assets/562e158d-4fa2-4f4e-ad45-336e0d5b3b3f" />


## Review

* Don't understand the filtering system, find it a bit rocky to use the plugin
<mark> Likely due to my incompetence in the area. Still able to get the basics of physical cable connections. </mark>
* I reckon the display could be better :
  - Clearer icons
  - Add icons for WAN routers,  vspheres
<mark> Can use custom images/icons. </mark>
  - Maybe have names with icons
<mark> Toggle 'Node Label items'. Currently using Device type and site. </mark>
  - Within rack display could be better
 * Can download PNG of topology
 * Can rearrange by dragging - though they don't alweays stay where you want, very 'floaty'
<mark> Fixed by adjusting plugin configurations (in plugins.py) to allow coordinate saving. </mark>
 * can group by sites and racks as well as filter
 * Want to add more data to understand/ explore better


