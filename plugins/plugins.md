Packaged Django apps that can be installed alongside NetBox to provide custom functionality 
not present in the core appliation.


Utilise plugins with netbox-docker created by users within the Netbox Community on github by creating a custom 
docker image : https://github.com/netbox-community/netbox-docker/wiki/Using-Netbox-Plugins.


## Capabilities
* Add new data models (tables in the SQL database)
* Add new URLs and views (browsable user views under /plugins rootpath)
* Add content to existing model templates
* Add navigation menu items - buttons/tabs ...
* Add custom middleware (software that acts as a bridge , enabling
   communication and interaction between different applications, systems or services)
* Declare configuration parameters
* Specify a min/max NetBox version for which it is compatible


## Limitations
Interaction of plugins with NetBox core is restricted in certain ways

Unable to : 
* Modify core models
* Register URLs outside the /plugins root
* Override core templates
* Modify core settings
* Disable core components
