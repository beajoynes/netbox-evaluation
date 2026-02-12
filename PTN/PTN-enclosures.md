Enclosures cover a range of objects which I have chosen to model these as two main object types :
* Data centres (Location)
* Brick building (Location)
* Customer building (Location)
* T cabinet (Location)
* 600 cabinet (Rack)
* Equipment rack (Rack)
* 1830 DCM shelf (Rack)


### Add field choices to configuration.py
```
FIELD_CHOICES = {
  ...
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


### Add object types to custom fields
* NL_UID (Location & Rack)
* 
