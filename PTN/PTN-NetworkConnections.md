Data extract fields :
* Connection Type - All 'Network Link', won't input into Netbox
* TrafficType - Custom field 
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
