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

