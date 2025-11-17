# netbox-floorplan-plugin

A netbox plugin providing floorplan mapping capability for locations and sites
* https://github.com/netbox-community/netbox-floorplan-plugin

Useful - currently we have floor plans of all sites? Baz Chandler/ Ade Prattley

* Needs to be manually set up, but is it able to know what devices/racks and measurements from the site data?
* Then the user just has to place it int he right place?


* provides graphical ability to draw racks & unracked devices on a floorplan
* support for metadata such as labels, areas, walls, coloring
* floorplan object mapped to sites or locations and click through rack/devices
* keyboard controls supported
* export to svg

# Installation
In netbox-docker directory: 
`nano plugin_requirements.txt.` add netbox-floorplan-plugin

`nano configuration/plugins.py` :
```
PLUGINS = ["netbox_floorplan"]
```

## Build and deploy
```
docker compose build --no-cache
docker compose up -d
```

# Review
* Compre to current floorplans
* In order for racks to display properly, the rack type of the rack should be specified and a width/height set within the type
* Floorplan dimensions can be set (rectanlge shape only?), metres or feet
* Can assign image as background - could upload current floorplans and leave at that? - not sure exactly how? Upload image to site first?
* 

# Use
* Currently floorplans are stored in DWG format but the 'public' format is PDF
* - DWG files are binary files used for containing 2D and 3D design data (vector graphics), closely associated with CAD programs.
  - SVG is a popular tool for displaying 2d graphics, charts and illustrtations on websties. A vectror file, can be scaled up or down without losing any resolution.
