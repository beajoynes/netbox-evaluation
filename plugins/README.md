Packaged Django apps that can be installed alongside NetBox to provide custom functionality 
not present in the core appliation.

# Installation (Netbox Docker)

Utilise plugins with netbox-docker created by users (within the Netbox Community*) on github by creating a custom 
docker image : https://github.com/netbox-community/netbox-docker/wiki/Using-Netbox-Plugins.

* Has also worked with the branching plugin from netboxlabs

NetBox installed to container (netbox-docker) by creating a custom docker image
## Demo with netbox-topology-plugin
Here I have ran through the install of the topology views plugin, this is done from having no plugins installed. 

Once you have created the `plugins_requirements.txt`, `Dockerfile-plugins` and `docker-compose.override.yml` files, they can be reused for all plugins (just add other plugins below) and the latter two don't need reconfiguring for each plugin. 

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

### Build and start 
```
docker compose build --no-cache
docker compose up -d
```

Navigate to netbox UI and there is now a Topology Views tab in the menu.




# Examples :
https://netboxlabs.com/plugins/
* **Validity** : Validity is the NetBox plugin to write "auto tests" for your network devices. You define compliance tests and Validity checks device state or configuration against these tests. Main use cases : configuration compliance and pre/post configuration checks.
* **Documents** : Faciliate the storage of site, circuit, device type and device specific documents within NetBox
* **Interface synchronisation** : Allows you to compare and synchronize interface names and types between devices and device types in NetBox. It can be useful for finding and correcting inconsistencies between interfaces when changing the device type.
* **Nbservice**: ITSM mapping.
* **NetBox Healthcheck** : Provides health check monitors that can be queried to make sure that the service is running in good condition.
* **Secrets** : Stores secrets in the database encrypted with a public key, can assign to any object, inlcuding contacts to associate them with a asecret (e.g. SSH key).
* **Inventory** : Keep track of hardware, whether it is installed or in storage.
* **Lifecycle** : Hardware EOL/EOS, License and support contract tracking.
* **Data flows** : Document data flows between devices and applications.
* **Branching** : Branching support to stage, review and collaborate on changes before applying them.
  
## Levels
There are 3 levesl to netbox plugins :
* Official : Certified plugins that are fully supported and owned by NetBox, have documentation with NetBox
* Certified : Plugins that meet criterea for quality, compatibility and ongoing maintenance - supported on NetBox Cloud and NetBox Enterprise
* Compatible : Community developed plugins that have been validated on NetBox cloud and/or NetBox Enterprise


# Capabilities
* Add new data models (tables in the SQL database)
* Add new URLs and views (browsable user views under /plugins rootpath)
* Add content to existing model templates
* Add navigation menu items - buttons/tabs ...
* Add custom middleware (software that acts as a bridge , enabling
   communication and interaction between different applications, systems or services)
* Declare configuration parameters
* Specify a min/max NetBox version for which it is compatible


# Limitations
Interaction of plugins with NetBox core is restricted in certain ways

Unable to : 
* Modify core models
* Register URLs outside the /plugins root
* Override core templates
* Modify core settings
* Disable core components


# Plugin backups ??
