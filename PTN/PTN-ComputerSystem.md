New sheet should have all the data!

### Fields
* ReconId - Custom field
* Status - status (need to update custom field in config)
* AssetID - NL_UID
* Category - Selection : Physical component, (Blank) -- custom field
* Type - Selection : Hardware, Processing unit, Server, Transmission, (Blank) -- custom field
* Item - Selection : Blade system, Card, Device, Port, Desktop, Processing unit, Server, Virtual Machine, (Blank) -- custom field or not included as it is object type??
* ManufacturerName - Need to add : 
* Model
* VersionNumber
* Name
* ShortDescription
* Span
* PCXConfigNumber
* StringName
* StringPosition
* IPAddress
* Chassis
* Rack
* CabinetName
* Location
* Chassis_reconid
* Rack_reconid
* Cabinet_reconid
* Location_reconid
* CITag
* HostName
* TSA
* TSB
* ElectronicAddress
* PCXDomain
* Region
* Status_Reason
* PrimaryCapability



### Netbox Fields 
* ReconId
* status
* cf_NL_UID
* role
* Item
* manufacturer
* device_type
* name
* description	Span	StringName	StringPosition	IPAddress	Chassis	Rack	CabinetName	Location	Chassis_reconid	Rack_reconid	Cabinet_reconid	Location_reconid	HostName	TSA	TSB	ElectronicAddress	PCXDomain	Region	Status_Reason	PrimaryCapability		

Repopulate Netbox ?!

Filter the 'item' column to show devices only. 
