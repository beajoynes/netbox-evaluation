# Branching plugin - [netbox-branching](https://github.com/netboxlabs/netbox-branching)

[Officicial NetBox extensions branching docs](https://netboxlabs.com/docs/extensions/branching/) 

## Description
A netbox plugin that introduces branching functionality - this is now an 'official' NetBoxLabs plugin so it is owned and 
supported fully by NetBox themselves.
Allows for the creation of a discrete snapshot f the NetBox database which can be modified independently before later being
merged back into the `main` branch. 
 
## Use case
Use to make changes to the service network without interferring with it's integrity. The `main` branch can be locked and branches need to go through approval/review before being merged, reducing the chances of mistakes being made to the actual network.

## Requirements
* NetBox v4.3 or later
* PostgreSQL 12 or later

## Official
* Certified, owned and supported by NetBox Labs

## Test priority 
* High

## Test Completed	

* Bea 24-11-2025

# Review 
* Very useful concept - definitely use this one
* Can see when adn who merged a branch, changes made etc
* Can restrict number of (working) branches that can exist simultaneously (default is no maximum)
* Can activate and deactivate branches using REST API - it will be provisioned automatically (same as UI)


 # Questions (and some answers)
* What is 'sync' vs merge'? Sync seems to produce errors if main branch changed, nut in the error it suggests to sync??? It should mean changes to main branch are synced to current branch - SYNC WORKS FOR UNRELATED CHANGES ONLY!
* How do I 'lock' the main branch, and allocate permissions/ levels of approval to branch merging?
* - In configuration : `main_schema` (default public) ? and `merge_validators`
* What counts as a conflict? What is it checking pre merge?


# Installation

* In `plugin_requirements.txt`, the plugin is named `netboxlabs-netbox-branching`
* In `congifuration/plugins.py`, reference `"netbox_branching"`
* **Unique requirement** : In `configuration/configuration.py`, need to ensure DATABASES is wrapped by `DynamicSchemaDict()`
 and add `DATABASE_ROUTER` after:
  ```
    from netbox_branching.utilities import DynamicSchemaDict

    DATABASES = DynamicSchemaDict({
      'default': {
          'ENGINE': 'django.db.backends.postgresql',
          'NAME': 'netbox',               # Database name
          'USER': 'netbox',               # PostgreSQL username
          'PASSWORD': 'password',         # PostgreSQL password
          'HOST': 'localhost',            # Database server
          'PORT': '',                     # Database port (leave blank for default)
          'CONN_MAX_AGE': 300,            # Max database connection age
      }
    })


    DATABASE_ROUTERS = [
      'netbox_branching.database.BranchAwareRouter',
    ]
  ```

### Menu view : 
<img width="888" height="141" alt="image" src="https://github.com/user-attachments/assets/9903defb-c774-4543-8d1a-a7fc7f7ace00" />


# Test
Working in main branch, option to 'create a branch' : 
<img width="904" height="622" alt="image" src="https://github.com/user-attachments/assets/4896ace8-0743-4d6d-a08c-a161c993dbef" />

'Create a branch' page :
<img width="904" height="786" alt="image" src="https://github.com/user-attachments/assets/24ecde5e-195d-4b89-9ff7-e23dfb489133" />


Branch page (still 'working' in main branch) :
<img width="900" height="826" alt="image" src="https://github.com/user-attachments/assets/281703d0-8812-4951-a9f7-51d84d47707f" />
Branch has :  a unique Schema ID, status,(description), Owner, Last synced, Last activity

May need to reload page to recognise new branch.

Switch to new branch :
<img width="909" height="914" alt="image" src="https://github.com/user-attachments/assets/fbb6d3ad-0449-4afd-864c-ad82c7f19f2e" />

Notification of branch being activated once switched
> **Note:** Double (duplicated) pop up message of activation. Minor issue that does not affect use.

Add in site, rack and device :
<img width="889" height="913" alt="image" src="https://github.com/user-attachments/assets/a74fcdde-79e8-497c-9645-d8bd6097ed12" />
Created as normal, just ensure you are in the correct branch (top right corner).


Navigate to branches tab from menu, click on branch :
<img width="901" height="910" alt="image" src="https://github.com/user-attachments/assets/05d9244e-5a98-4f28-a837-a1fc32467962" />
Updated with sync, activity, and changes (compared to main).

Merge allows for dry run and checks for conflict changes : 
<img width="909" height="390" alt="image" src="https://github.com/user-attachments/assets/ae67dbf3-e05b-4b10-98fa-b1a328081fd2" />

If there are conflicts and you attempt a dry run  (added a site called Reading in main branch) :
<img width="894" height="334" alt="image" src="https://github.com/user-attachments/assets/95ee00f9-fa10-4cad-b46c-07217d483894" />

Jobs tab of branch, Job 52 is the dry run of merging the branch successfully, 53 is the actual merge (commit changes checked).
<img width="899" height="531" alt="image" src="https://github.com/user-attachments/assets/a565ce39-7604-4742-b777-7695784332d7" />


Once merged, no longer have the option to swtich to the branch (or activate) : 
<img width="905" height="920" alt="image" src="https://github.com/user-attachments/assets/3a0f7123-0fea-4020-96e2-ac893f5b1bc0" />

Branch status is now 'Merged'. 'Revert' option allows you to revert back to the state before the merge, main will go back to its pre-merge state and the branch will be reactivated.
