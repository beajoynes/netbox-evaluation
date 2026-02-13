Enclosures cover a range of objects which I have chosen to model these as two main object types :
* Data centres (Location)
* Brick building (Location)
* Customer building (Location)
* T cabinet (Location)
* 600 cabinet (Rack)
* Equipment rack (Rack)
* 1830 DCM shelf (Rack)


I spent a while trying to decide the best protocol for enclosures, with their parent-child relationships.


Given Data Centres, Building Brick, Customer Building and T cabinet don't appear as parent enclosures for active equipment, I am considering them as locations with the other types being modelled as racks.


My other thought was creating a custom object but I thought it best to keep it as simple as possible and work with core Netbox.


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

## LOCATIONS

### Add object types to custom fields
* NL_UID 
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
* Barcode, Text, ^\d{12}$, unique

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

## RACKS

### Add object types to custom fields
* NL_UID
* Road
* MP
* CW
* MP Offset
* Barcode
* Span
* Installation Date
* NRTS ID
* TAF

### Create custom fields
* Parent_enclosure (Parent enclosure), Object (rack)

### Manually add manufacturers and rack types 
Manufacturers
* Generic
* Nokia

Rack type  (After checking the product catalogue shared with me by Karl G, I couldn't get data on the 'form factor' - a required field for rack types in Netbox - so this is guess work)
* 1830 DCM shelf, Nokia, 2-post frame
* Equipment rack, Generic, 4-post frame
* 600 Cabinet, Generic, 4-post cabinet

### csv headers () 
In Netbox, racks require a site value, could explore the parent-child field object relation I made later on? For now I am adding in sites to the spreadsheet where they aren't already there.

Parent racks and child racks on separate sheets so the parent racks exist on import. Parent enclosures are referenced by their rack object ID (number only). Need to find 

