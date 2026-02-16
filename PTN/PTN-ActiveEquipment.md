Active Equipment

## Devices

### Add object types to custom fields
* NL_UID
* Road
* MP
* CW
* MP Offset
* Span
* NRTS ID
* TAF
* installation date

Custom field choices:
* Stack name
```
XRC1-EX43-005
XDC1-EX43-001
XDC1-SR15-001
XDC1-EX43-002
XDC2-EX43-001
XDC4-SR15-001
XDC2-EX43-002
XRC2-EX43-001
XRC2-SR41-001
XRC2-EX43-002
XRC1-EX43-001
XRC1-EX43-002
XRC1-SR15-001
XMJ2-EX43-002
XMJ1-EX43-002
XMJ3-EX43-002
XRC2-EX43-004
XRC1-EX43-003
XRC1-EX43-004
XMN2-EX43-002
XMN1-EX43-002
XMJ3-XMJ3-VE1S-02
```

UPDATE NETBOX CONFIGURATION.PY FILE !!!

Create custom fields 
* Age_at_Install (Age at Install) - Not done as not filled out in data extract
* Critical_asset (Critical Asset), Boolean
* Stack_name (Stack name), selection
* Stack_position (stack position), integer
* String_name (String name),  Text
* String_position (String position), integer


* String name - text or selection ??
* string position - integer


### Bulk import of Device Roles using Direct Import

Modelled as the 'type' from the product catalogue

```
name, slug, color
Transmission, transmission, 6e6d6d
Processing unit, processing-unit, 830715
Storage, storage, cdcc81
Server, server, 8f81cd
```


### Manufacturer bulk import via direct import
```
name, slug
Antrica, antrica
Moxa, moxa
Hewlett Packard Enterprise,hpe
Juniper, juniper
Advantech, advantech
Actelis, actelis
RAD Data Communications, rad-data-com
Verint, verint
Alcatel Lucent, alcatel-lucent
Kenton, kenton
Radwin, radwin
AMG Systems, amg-systems
```

### Device types

* manufacturer, model, slug, u_height

The height I have assumed as 1 rack unit (1.75 in) due to an incomplete and difficult to navigate product catalogue - except for the following that I could find eventually :
* MX480 (8)
* 1830 PSS-32 (14)
* Verint NVR (10)
* EX4300s (1)


### Devices 
Parent device will be represented by the netbox built in 'device bay' object.

> **Note**
> Bulk import requires manufacturer but manually adding does not. ????


Unfilled Fields
* Left out IPAM for now 
* Left out any fully blank columns also
* PCX - not got much filled, 4 records
* = SW Cluster ????
* = ManagedBy ????
* = PCX Config Number ????
* = PCX Domain ????


### csv headers
* cf_NL_UID  = NL UID
* manufacturer
* device_type = Product Name
* name = Name
* status = Asset Status  -- ensure the statuses are updated to the correct import value
* owner = Owner
* site = REQUIRED BY NETBOX -- Not in the active equipment data extract * 
* rack = Parent Enclosure
* device_bay = Parent Equipment
* cf_Barcode = Barcode
* serial = Serial Number
* cf_Installation_date = Installation Date
* cf_Critical_Asset = Critical Asset
* cf_Stack_name = Stack Name
* cf_Stack_position = Stack Position
* cf_String_Name = String Name
* cf_String_Position = String Position
* cf_NRTS_ID = NRTS ID
* cf_TAF = TAF

### * sites  (and racks of child equipment)
Sites are a required field in Netbox, yet there is not currently a field in the ECM.

Thinking of using the enclosures field and corresponding sheet to auto fill the site field.

`=XLOOKUP(G2, 'PTN rack (parents)'!C2:C32, 'PTN rack (parents)'!F2:F32)`
=
Works fine but error for the shelf / child racks - this is expected as it refers to a separate sheet. Simply use the following in those error cells :

`=XLOOKUP(G38, 'PTN rack (children)'!C:C, 'PTN rack (children)'!F:F)`

Also have an error where there are child equipment that don't have 'rack' filled out, should be able to fill these missing rack values out in a similar way to sites.

`=XLOOKUP(H149, C:C, G:G)`

### Find & Replace (in-place change) -- For device types that have a trailing ':' for location reference
'''
Select the whole column.

Press Ctrl + H (Find and Replace).

In “Find what”, type:

text
:*
Leave “Replace with” completely empty.

Click “Replace All”.
'''
> '*' is a wildcard meaning “any characters after this”, so this removes the colon and everything after it in each selected cell.

### manufacturer 
Annoyingly this is also required in Netbox despite device types having this information already inputted (worth bringing up with them?) but can use  `XLOOKUP` again to find them from the device type sheet.
