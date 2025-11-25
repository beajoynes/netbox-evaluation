# Netbox Plugin - [netbox-floorplan-plugin](https://github.com/netbox-community/netbox-floorplan-plugin)

## Description	

A netbox plugin for modelling and managing documents related to the 'out of the box' objects in NetBox.

## Use Case	
Documents can be stored against many object types, with a wide range of file types supported (notably : png, jpeg, pdf, doc(x),txt) .  

## Compatible Version	

| NetBox Version	| Plugin Version |
|----------------|----------------|
| 4.3+	| 0.7.4 |
| 4.2+	| 0.7.2 |
| 4.0 - 4.2 | 0.7.0 |
| 3.6+ | 0.6.4 |
| 3.5.x	| 0.6.0 |
| 3.3.x - 3.4.x	| 0.5.1 |

## Certified	

* Compatible

## Test Priority	

* High
  
## Test Completed	

## Review
* Is the attatchments plugin better for our use? - Allows attatchment of files to any object (including plugins, for example) but less information is given in it's github page (i.e. file types etc)

## Installation

Optional plugin configs (`congifuration/plugins.py`)

```
PLUGINS_CONFIG = {
     'netbox_documents': {
         # Enable the management of site specific documents (True/False)
         'enable_site_documents': True,
         # Enable the management of location specific documents (True/False)
         'enable_location_documents': True,
         # Enable the management of circuit specific documents (True/False)
         'enable_circuit_documents': True,
         # Enable the management of device specific documents (True/False)
         'enable_device_documents': True,
         # Enable the management of device type specific documents (True/False)
         'enable_device_type_documents': True,
         # Enable the management of module type specific documents (True/False)
         'enable_module_type_documents': True,
         # Enable the global menu options (True/False)   
         'enable_navigation_menu': True,
         # Location to inject the document widget in the site view (left/right)
         'site_documents_location': 'left',
         # Location to inject the document widget in the location view (left/right)
         'location_documents_location': 'left',
         # Location to inject the document widget in the device view (left/right
         'device_documents_location': 'left',
         # Location to inject the document type widget in the device type view (left/right
         'device_type_documents_location': 'left',
         # Location to inject the document widget in the device view (left/right
         'circuit_documents_location': 'left'
     }
}
```

