A plugin to allow the ability to reorder rack units in NetBox using a drag and drop interface. 
Tested on google cloud virtual machine (test1) using netbox docker. 
Tested install alongside topology plugin to test multiple plugins and reinforce installation with NetBox docker.

# Intallation

`nano plugin_requirements.txt` add netbox-reorder-rack

`Dockerfile-Plugins` No need to update as file already exists (from topology install). This Dockerfile is used to build the custom image, 
it points to the plugin_requirements.txt, configuration.py and plugin.py files which will have the relevant information about which plugin
is being installed.

`docker-compose.override.yml` Same as above, already correct to point to the files which we need to update anbd 
