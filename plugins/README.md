Packaged Django apps that can be installed alongside NetBox to provide custom functionality 
not present in the core appliation.


Utilise plugins with netbox-docker created by users within the Netbox Community on github by creating a custom 
docker image : https://github.com/netbox-community/netbox-docker/wiki/Using-Netbox-Plugins.

## Plugins examples :
* Validity : Validity is the NetBox plugin to write "auto tests" for your network devices. You define compliance tests and Validity checks device state or configuration against these tests. Main use cases : configuration compliance and pre/post configuration checks.
* Documents : Faciliate the storage of site, circuit, device type and device specific documents within NetBox
* Interface synchronisation : Allows you to compare and synchronize interface names and types between devices and device types in NetBox. It can be useful for finding and correcting inconsistencies between interfaces when changing the device type.
* Nbservice: ITSM mapping.
* NetBox Healthcheck : Provides health check monitors that can be queried to make sure that the service is running in good condition.
* Secrets : Stroes secrets in the database encrypted with a public key, can assign to any object, inlcuding contacts to associate them with a asecret (e.g. SSH key).
* Inventory : Keep track of hardware, whether it is installed or in storage.
* Lifecycle : Hardware EOL/EOS, License and support contract tracking.
* Data flows : Document data flows between devices and applications.
  


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


# Plugin backups ??
