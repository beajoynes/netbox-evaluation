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
* Road
* MP
* CW
* MP Offset
* Span
* NRTS ID
* TAF


### Create custom fields
* Installation_date (Installation date), Date
> NOTE: ISO 8601 format : YYYY-MM-DD - Use DATEVALUE function in excel
* Enclosure_label (Enclosure label), Text
* Barcode, Text, ^\d{12}$

### csv headings 
* cf_NL_UID	facility
* name
* slug
* status
* owner
* site
* parent
* cf_Road
* cf_Marker_Post
* cf_CW	cf_MP_Offset
* cf_Enclosure_label
* cf_Barcode
* cf_Span
* cf_Installation_date
* comments
* cf_NRTS_ID
* cf_TAF			

### Bulk import
* Check date format
* Check digit format - make text (barcode)
* Open / edit with Notepad after exporting as csv - remove extra columns if needed, check all data is in correct format
