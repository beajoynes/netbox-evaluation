Everything sites

* Field choices (DCIM.sites.status) in configuration.py
* Manually add site groups : Roadside sites, Tx sites
* Custom field choices
* Custom fields
* Sites by csv file

### Custom field choices (choice sets) 

* CW choice
```
A:A
B:B
J:J
K:K
L:L
M:M
  ```

* Hardshoulder choices
```
Compound:Compound
```

* Road choices
```
Mx:Mx
Mx2:Mx2
Mx3:Mx3
```

* SPC choices
```
SPC A:SPC A
SPC B:SPC B
SPC C:SPC C
SPC D:SPC D
SPC E (MM Lite):SPC E (MM Lite)
SPC F (E.g. A14):SPC F (E.g. A14)
SPC ATMg:SPC ATMg
```

### Custom fields
* NL_UID  (NL UID), Text, Required, Unique
* CW (CW), Carriageway, Selection, CW choice set
* Hardshoulder, selection, Hardshoulder choice set
* NRTS_ID (NRTS ID), Text
* TAF (TAF), Text
* SPC (SPC), Service Provisioning Capability, SPC choices
* Span, Text, ^(?=.*\d.*\d.*\d).+$
* Road, Location, Selection, Road choices
* Marker_Post (Marker Post), Location, Decimal, 125 (Display weight)
* MP_Offset (MP Offset), Location, Distance from marker post (0-100m), Integer, 0, 100, 150 (Display weight)

### Manually add :
* site groups : Roadside sites, Tx sites
* owners : NRTS, Non NRTS
* regions - exported csv of names and slugs from original DB

### csv headers (19) AKA site fields
* cf_NL_UID
* group
* name
* slug
* status
* cf_Road
* cf_Marker_Post
* cf_CW
* cf_MP_Offset
* cf_Hardshoulder
* region
* cf_Span	cf_SPC
* latitude
* longitude
* owner
* physical_address
* cf_NRTS_ID	cf_TAF

The csv is used to upload to netbox as a bulk import in the UI
