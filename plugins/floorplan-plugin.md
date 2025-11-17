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
* Compare to current floorplans :  Maybe not quite ready as there is a lack of usability/ customisation and a couple issues in design stage, but a feesable option with fairly simple coding to make work if it would be of use?
* In order for racks to display properly, the rack type of the rack should be specified and a width/height set within the type
* Floorplan dimensions can be set (rectanlge shape only?), metres or feet
* - Displayed at bottom of plans, can't toggle off or move?
* Can assign image as background - should be simple to code changing back ground colour atleast?
* - Attempt with Dover site (added image)
  - could upload current floorplans and leave at that?
  - not sure exactly how?
  - Upload image to site first? Tried but doesn't work.
* Can only add racks etc if populated in the site - nto just sandbox - good as limits chances of mistakes
* Can add walls, areas and labels
* - Drag and drop, resize, set colour (detailed range)
  - Can't put in dimensions 
  - Lock/unlock object : stops it from being moved even after clicking on it
  - Object layer control (forwards/backwards)
  - No specific shape objects e.g. door, chair
  - Maybe would be good to be able to display a key to show any colour coding if used?
  - A grid could be useful also?
* Zoom
* Floorplan with site with racks populated (Hemel Hempsted data centre)
* - Adding racks appears as default in black (same as back ground) and cannot change rack colour - should be simple to code but currenty not great, though can just add 'area' behind.
  - Cannot change colour of text or how it is shown either.
  - Displays rack name vertically on saving
  - Also shows status horizontally in blue over the top - updated automatically if status is updated
* In saved floorplan, clicking on a rack takes you to its page/details!
* Not got any info on how to use on github repository, though it is mainly straight forward

# Use
* Currently floorplans are stored in DWG format but the 'public' format is PDF
* - DWG files are binary files used for containing 2D and 3D design data (vector graphics), closely associated with CAD programs.
  - SVG is a popular tool for displaying 2d graphics, charts and illustrtations on websties. A vectror file, can be scaled up or down without losing any resolution.
* Easy to edit when a change occurs (e.g rack added/removed)
* Really like how the racks populated are there to add and status is automatically updated.
* clicking on a rack takes you to its page/details!
