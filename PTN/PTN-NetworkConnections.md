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
COLE-SWCH-01-PTN	 ge-0/0/10  1000base-t
PTN WL APN Gateway	Core1	1000base-t
PTN WL APN Gateway	Core2	1000base-t
XMJ1-XMJ2-M540-02-010	ETH-5	1000base-t
XMJ1-XMJ2-M540-02-010	ETH-6	1000base-t
XMJ1-XMJ2-M540-03-010	ETH-5	1000base-t
XMJ1-XMJ2-M540-03-030	ETH-6	1000base-t
XMJ1-XMJ2-M540-08-010,ETH-5,1000base-t
XMJ1-XMJ2-M540-08-040,ETH-6,1000base-t
XMJ1-XMJ2-VE1S-01-012,P3,1000base-t
XMJ1-XMN1-M540-04-020,ETH-6,1000base-t
XMJ1-XMN1-SA8X-04-930,8,1000base-t
XMJ1-XRC1-EX43-01-030,xe-0/2/0,1000base-t
```
The above entries contains a device that does not exist in the PTN, I believe one is a connection to the COLE Switch - essentially connecting the PTN to the NRTS network ?
For now I have deleted them from my sheet but wanted to keep a record here.


So many are missing??? why is this??
