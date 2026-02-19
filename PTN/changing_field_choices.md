Assuming install is as set out following the instructions as written in [].

Navigate to the Netbox-Docker directory, there should be a directory named 'configuration' and within that a file named 'configuration.py'.

Use an editor of your choice to open and edit this file ( E.G. `nano configuration/configuration.py` )

At the end of the page add the following :
```
FIELD_CHOICES = {
    'dcim.Site.status': (
        ('decommissioned', 'Decommissioned', 'red'),
        ('in_service', 'In Service', 'green'),
        ('commissioned', 'Commissioned', 'yellow'),
    )
}
```

> **NOTE** : The first choice will be the default


### All the field choices I added
```
FIELD_CHOICES = {
    'dcim.Site.status': (
        ('in_service', 'In Service', 'green'),
        ('decommissioned', 'Decommissioned', 'red'),
        ('commissioned', 'Commissioned', 'yellow'),
    ),

    'dcim.device.status': (
        ('in_service', 'In Service', 'green'),
        ('decommissioned', 'Decommissioned', 'red'),
        ('commissioned', 'Commissioned', 'yellow'),
    ),
    'dcim.location.status': (
        ('in_service', 'In Service', 'green'),
        ('decommissioned', 'Decommissioned', 'red'),
        ('commissioned', 'Commissioned', 'yellow'),
    ),
    'dcim.rack.status': (
        ('in_service', 'In Service', 'green'),
        ('decommissioned', 'Decommissioned', 'red'),
        ('commissioned', 'Commissioned', 'yellow'),
    )

}
```
