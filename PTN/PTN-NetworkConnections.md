Data extract fields :
* Connection Type - All 'Network Link', won't input into Netbox
* TrafficType - Custom field (cf_Traffic_type)
* Source Device 
* Source Port - Netbox has device components : Interfaces, Console ports, Front ports, Rear ports, ... -- which is best? ASKED KARL 
* Dest Device
* Dest Port - "" 

Netbox required fields:
* side_a_device = Source device
* side_a_type =   -- depends on the type of device component 
* side_a_name = Source port
* side_b_device = Destination device
* side_b_type = 
* side_b_name = Destination port

### Traffic type

Custom field choices 
```
Traffic
3rd Party IF HBW
Management
Control
3rd Party IF LBW
```

Custom field
* Traffic_type
* Selection
* Traffic type
* Choiceset traffic types


### Interfaces

Created a sheet 'PTN interfaces' with the column headers as the required fields for Netbox : device, name and type.
Device and name can be filled out by copying both (Source and Destination) device columns from the data extract as well as both (Source and Destination) port columns.

Interface type can be selected from an extensive range, of which for now I am putting all interfaces as '1000base-t' while still unsure of the true types.

```
COLE-SWCH-01-PTN  |	 ge-0/0/10	 |  1000base-t
```
The above entry contains a device that does not exist in the PTN, I believe it is a connection to the COLE Switch - essentially connecting the PTN to the NRTS network ?
For now I have deleted it from my sheet but wanted to keep a record here.
