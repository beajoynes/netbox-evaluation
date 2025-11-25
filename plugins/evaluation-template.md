# Netbox Plugin - [netbox-floorplan-plugin](https://github.com/netbox-community/netbox-floorplan-plugin)

## Description	

A netbox plugin providing floorplan mapping capability for locations and sites.

## Use Case	

We currently use autocad for site mapping, to show where racks are installed inside a building.

## Compatible Version	

| NetBox Version	| Plugin Version |
|----------------|----------------|
| 3.5	| >= 0.3.2 |
| 3.6	| >= 0.3.2 |
| 4.0.x	| 0.4.1 |
| 4.1.x	| 0.5.0 |
| 4.2.x	| 0.6.0 |
| 4.3.x	| 0.7.0 |
| 4.4.x	| 0.8.0 |

## Certified	

* Certified by Netbox Labs

## Test Priority	

* High
  
## Test Completed	

* Bea 24-11-2025
  
## Evaluation Comments

* Provides graphical ability to draw racks & unracked devices on a floorplan
* Support for metadata such as labels, areas, walls, coloring
* Floorplan object mapped to sites or locations and click through rack/devices
* Keyboard controls supported
* Eexport to svg
* Compare to current floorplans :  Maybe not quite ready as there is a lack of usability/ customisation and a couple issues in design stage, but a feesable option with fairly simple coding to make work if it would be of use?
* In order for racks to display properly, the rack type of the rack should be specified and a width/height set within the type
* Floorplan dimensions can be set (rectangle shape only?), metres or feet
* - Displayed at bottom of plans, can't toggle off or move?
* Can assign image as background - should be simple to code changing back ground colour atleast?
  - Attempt with Dover site (added image)
  - could upload current floorplans and leave at that?
  - not sure exactly how?
  - Upload image to site first? Tried but doesn't work.
* Can only add racks etc if populated in the site - nto just sandbox - good as limits chances of mistakes
* Can add walls, areas and labels
  - Drag and drop, resize, set colour (detailed range)
  - Can't put in dimensions 
  - Lock/unlock object : stops it from being moved even after clicking on it
  - Object layer control (forwards/backwards)
  - No specific shape objects e.g. door, chair
  - Maybe would be good to be able to display a key to show any colour coding if used?
  - A grid could be useful also?
* Zoom
* Floorplan with site with racks populated (Hemel Hempsted data centre)
  - Adding racks appears as default in black (same as back ground) and cannot change rack colour - should be simple to code but currenty not great, though can just add 'area' behind.
  - Cannot change colour of text or how it is shown either.
  - Displays rack name vertically on saving
  - Also shows status horizontally in blue over the top - updated automatically if status is updated
* In saved floorplan, clicking on a rack takes you to its page/details!
* Not got any info on how to use on github repository, though it is mainly straight forward

## Review

* Currently floorplans are stored in DWG format but the 'public' format is PDF
  - DWG files are binary files used for containing 2D and 3D design data (vector graphics), closely associated with CAD programs
  - SVG is a popular tool for displaying 2d graphics, charts and illustrtations on websties. A vectror file, can be scaled up or down without losing any resolution.
* Easy to edit when a change occurs (e.g rack added/removed)
* Really like how the racks populated are there to add and status is automatically updated.
* Clicking on a rack takes you to its page/details!
  
## Next actions

* Do we currently have floor plans of all sites? 
* Reach out to Baz Chandler/ Ade Prattley for more info.
* Needs to be manually set up, but is it able to know what devices/racks and measurements from the site data?
* Then the user just has to place it int he right place?


# Installation

Utilise plugins with netbox-docker created by users (within the Netbox Community*) on github by creating a custom 
docker image : https://github.com/netbox-community/netbox-docker/wiki/Using-Netbox-Plugins.

* Has also worked with the branching plugin from netboxlabs

NetBox installed to container (netbox-docker) by creating a custom docker image
## Demo with netbox-topology-plugin
Here I have ran through the install of the topology views plugin, this is done from having no plugins installed. 

Once you have created the `plugins_requirements.txt`, `Dockerfile-plugins` and `docker-compose.override.yml` files, they can be reused for all plugins (just add other plugins as required) and the latter two don't need reconfiguring for each plugin at all. 

For the majority, only the `plugins_requirements.txt` and `configuration/plugins.py` need to be modified with each plugin - though check carefully for each plugin exactly how to do this (e.g. plugins_requirements.txt used '-' but configuration/plugins.py uses '_'), and if any other files need to be modified.

### Create and modify files in root folder 
`plugins_requirements.txt`
*  Add plugin `netbox-topology-views`

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

### Build and deploy 
```
docker compose build --no-cache
docker compose up -d
```

Navigate to netbox UI and there is now a Topology Views tab in the menu.


## Screenshots

<img width="989" height="717" alt="image" src="https://github.com/user-attachments/assets/6c5f8f75-4582-4537-b321-1c93bcdfca2f" />
