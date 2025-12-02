# netbox-evaluation
A repository to keep track of netbox learning, exploring and evaluation

Netbox community github : https://github.com/orgs/netbox-community/repositories?type=all

Netbox is a central nervous system or 'source of truth' for an entire network infrastructure.
* Central source of truth
* Solution for modeling and documenting mnetwork infrastructure
* Migrate from spreadsheets = fewer errors, ease of use
  
<img width="948" height="570" alt="image" src="https://github.com/user-attachments/assets/35207439-f9fd-4f01-8ea8-de30b17da0be" />


DCIM : Data centre infrastructure management

IPAM : IP address management


Can change setting of changelog display - but can't filter through changelog so well.


## Features
* Comprehensive data model
* Focused development
* Customisable
  - Plugins
  - Integrations : Netbox-zabbix-sync, REST API, Ansible
* Netbox backend : BACKUPS
* Image stroage, uploading, access, display?
* - Tested with Dover site, adding an image
  - Can see image previews, with name  - click on to see more details including decription, file details, parent object and changelog 


## Environments 
So far used a containerised version of NetBox : NetBox-docker.
Ran with :
* Google cloud virtual machine (ssh through Ubuntu-24.04)
* Ubuntu virtual machine on HyperV (ssh through WSL)
* ParrotOS virtual machine
* Alma virtual machine - used with an older version of NetBox (v3.3.2?)

### NetBox Docker
* Faster deployment
* Eliminate dependency conflicts - as all components are packaged into a single image, ran in it's own isolated environment
* Ensure consistent environments across development and testing
* Simplified upgrades
* Deploy with docker compose - single file


## Telent/ NRTS uses !!! Specific, Why use it? ....
* Update current network infrastructure records
* Saving time and reducing errors as multiple spreadsheets currently need to be updated when changes are made
* Central system

## Using / migrating to NetBox
NetBox docs on Getting started and planning to use NetBox : https://netboxlabs.com/docs/netbox/getting-started/planning/
* Identify current sources of truth
* Determine what to move - Although the current release might not support a particular type of object, there may be plans to add support for it in a future release
* Validate existing data
* Order of operations (recommended) - self nesting models (e.g. Tenant Group, Region, Site Group, Location) can have a recursive hierarchy, for example a region representing both countries and cities with cities nested under countries.

## Back ups
* Important!
* Backup to local machine
* Copying back ups to another machine
* Restoring back ups

## Plugin reviews
* Drag and drop reorder rack (also proof of multiple plugin use)
* Floorplan
* Topology
* branching

### Telent mini site (Topology plugin)
* MMLite scheme
* ALMY site - in site connectivity / racks + MTS to mts?
* Overall data

## Alternatives
* Device42
* Infoblox
