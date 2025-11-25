# [netbox-inventory](https://github.com/ArnesSI/netbox-inventory?tab=readme-ov-file)

## Description

Manage hardware inventory, both installed and in storage. Define assets that represent hardware that can be used as devices, modules, inventory item or rack in NetBox.  


## Plugin data model :
<img width="1641" height="1201" alt="image" src="https://github.com/user-attachments/assets/f189fbc6-d3fd-4acb-a16d-43eac49b7e93" />

## Use case
We have assets in storage - including spares and repairs, that need to be catalogued and kept track of. 

## Compatability

This plugin requires netbox version 4.3 to work. Older versions of the plugin support older netbox version as per table below:

| NetBox Version	| Plugin Version |
|----------------|----------------|
| 3.7 |	1.6.x |
| 4.0 |	2.0.x |
| 4.1	| 2.1.x,2.2.x |
| 4.2	| 2.3.x |
| 4.3	| 2.4.0 |
| 4.4	| >=2.4.1 |

## Review 

# Installation
 
* `plugin_requirements.txt` : Add `netbox-inventory`

* `configuration/plugins.py` : Add `"netbox_inventory"` to `PLUGINS = [ ]`

Inventory menu : 
<img width="345" height="452" alt="image" src="https://github.com/user-attachments/assets/55c92009-8ccc-4c5e-9245-7ceb6dd4ea86" />

Adding a new asset (including status options) : 
<img width="882" height="837" alt="image" src="https://github.com/user-attachments/assets/70c16cd0-6583-4365-8143-a8c4f7fd22b9" />

<img width="887" height="858" alt="image" src="https://github.com/user-attachments/assets/05339a70-f2ee-4348-a483-96f745bb01c1" />
