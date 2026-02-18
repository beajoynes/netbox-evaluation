New sheet should have all the data!

### Fields
* ReconId - Custom field
* Status - status (need to update custom field in config - add Deployed)
* AssetID - NL_UID
* Category - Selection : Physical component, (Blank) -- custom field
* Type - Selection : Hardware, Processing unit, Server, Transmission, (Blank) -- custom field
* Item - Selection : Blade system, Card, Device, Port, Desktop, Processing unit, Server, Virtual Machine, (Blank) -- custom field or not included as it is object type??
* ManufacturerName - Need to add : Netcomm, Siae, 
* Model - device_type
* VersionNumber - NO DATA
* Name - name
* ShortDescription - description
* Span - add to custom field span
* PCXConfigNumber - NO DATA
* StringName - add to custom field
* StringPosition - add to custom field
* IPAddress - only one, much simpler then all the IP data from other sheet
* Chassis - NO DATA for device
* Rack - rack
* CabinetName - rack / site ?? location ?
* Location - location
* Chassis_reconid - NOT NEEDED, Netbox embedded id / object relations
* Rack_reconid - NOT NEEDED
* Cabinet_reconid - NOT NEEDED
* Location_reconid - NOT NEEDED
* CITag - NO DATA
* HostName - NOT NEEDED, same as name?
* TSA - ??
* TSB - ?? 
* ElectronicAddress - NOT MUCH DATA
* PCXDomain - NO DATA
* Region - region, not all 'WMCC' ?!?! 268 WMCC, 26 ERCC
* Status_Reason - Same as status? Has all as 'In Service'
* PrimaryCapability - role !!!



### Netbox Fields 
* ReconId
* status
* cf_NL_UID
* role
* Item
* manufacturer
* device_type
* name
* description	-- Span	StringName	StringPosition	IPAddress	Chassis	Rack	CabinetName	Location	Chassis_reconid	Rack_reconid	Cabinet_reconid	Location_reconid	HostName	TSA	TSB	ElectronicAddress	PCXDomain	Region	Status_Reason	PrimaryCapability		


Repopulate Netbox ?!

Filter the 'item' column to show devices only. 

### Manufacturers
```
name,	slug
Juniper,	juniper
Antrica,	antrica
Nokia,	nokia
Actelis,	actelis
Advantech,	advantech
RAD Data Communications,	rad-data-communications
Simulation Systems Ltd,	simulation-systems-ltd
Kenton,	kenton
Moxa,	moxa
AMG Systems,	amg-systems
Radwin,	radwin
Siae,	siae
Verint,	verint
Hewlett Packard Enterprise,	hpe
Generic,	generic
Netcomm,	netcomm 
Alcatel Lucent,	alcatel-lucent
```
