* Important to still find out the difference / similarities between infrastructure scenarios and connectivity solutions
* What is alarm correlation and LOE exactly ?
* Is it possible to customise status options???? https://github.com/netbox-community/netbox/blob/main/docs/configuration/data-validation.md#field_choices


### Issues with current PTN
* Spreadsheet overload
* Confusing
* Different scenarios / connectivity solutions mixed
* Hard to update
* Need to use a different software to access drawings - No in built diagrams
* Different / inconsistent naming conventions - e.g spans
* Incomplete dataset
* Fields / acronyms people don't know the meaning of! (E.g. TM requirement)
* No population model document for NRTS 2 (There was for NRTS 1)
* Confusion of where dummy locations come into play/ how far it goes as lat/long exist

### Best practices for import
* fresh netbox instance
* Adjust configuration.py file as needed to change status field choices
* Add custom fields to netbox
* Manually add tenants, region, site groups, small objects
* Translate to Netbox friendly csv
* Proof check for correct names!! ETC
* Upload into netbox 
* How is exported  ??? QLIK V CMDB
  

### Netbox
* Field order
* Fresh instance for PTN?
* Certain objects depend upon other objects existing : 
* - Interfaces before connections
  - Site, Device role, Device type before Device 
  - 


### PTN
* Order of fields ? Importance
* Complete dataset needed??
*  - More important for live
   - barcode not used for example
   - similar ish serial numbers discovered from eq  uipment using smnp for example
   - Address not super necessary
* Do we need to sort by scenarios?
* Do we need to sort by connectivity solutions?
* Lat / Long is one less decimal place than the given PTN data
* - That is fine, within 4m
* Is data center a site type?
* - Tx site covers any site like that
  - Model
* String name example ?? Similar or same as span?? And position?
* - String of equipment connected between TS, inside RC/TS this is irrevelevant, resilient, generally same equipment but can be different, logical path between two sites
  - position , in increments of 10 (incase more needs to be added), string name means there must a be a string position
* Drawing number - is this linking to qlik or a drawing that can be attached?
* - Relationship to document for equipment , mcy (map view)  or cpf (equipment itsllf) drawing, not used for correlation and possibley not for LOE
* SW cluster??
* - Software cluster : For resilience chassis > blade > VMs in cluster such that if one goes down another can take over, a way of recording a logical  grouping  - not in active equpipment - in software
* Stack name - stack device to look like (for example) one big switch from 4 ex4300 switches reporting as opne, individual chassis making , generally position 0 is master
* PCX ? - only relevant for alcatel omnipcx equipment, sc11 ERTs
* - Config number : stored in manager by allocation of shelf number - unique per domain, country split into 2 domains : c and d to provide resilience, z is for testing dummy info
* What are the equipment components vs devices ?
* - chassis and sliding units, equip components are a level down from slide in units - don't have processing power
  - e.g. omnipcx gd, is a card
  - children of active equipment (some used for alarm correlation) mainly for inventory management
  - top few without parent equipment are network ports essentially - SFP small form factor plug, makes machines more configurable by plugging into get different speeds, inventory management - not used for alarm correlation
* Alarm correlation defined in TMIP interface
* - NRTS1 population model document but not for NRTS2
 

# Questions for Karl/Bryce

* Shelf
* TM requirement -- Bryce ?
* How set on status names ? Netbox v NRTS - Will the current statuses work
* - For some, dates back - important for billing. See about chagning it in NetBox itself
* what needs to relate ????
* What is parent equipment/ how does it work?
* Do postcodes need to be a separate field, or can it be included in the address? NOPE especially in PTN but not used live either
